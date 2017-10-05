---
title: "Azure Application Insights SDK ön işleme ve filtreleme | Microsoft Docs"
description: "Telemetri işlemciler ve SDK'sı Telemetri başlatıcıları filtre veya telemetri Application Insights portalına gönderilmeden önce veri özellikleri eklemek için yazın."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="0d1fc-103">Filtreleme ve Application Insights SDK'sı telemetri ön işleme</span><span class="sxs-lookup"><span data-stu-id="0d1fc-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="0d1fc-104">Yazma ve eklentiler nasıl telemetri yakalanan ve Application Insights hizmetine gönderilmeden önce işlenen özelleştirmek Application Insights SDK'sı için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="0d1fc-105">[Örnekleme](app-insights-sampling.md) , istatistikleri etkilemeden telemetri hacmini azaltır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="0d1fc-106">Birlikte tutar ilgili veri noktaları aralarında bir sorunu tanılamada gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="0d1fc-107">Portalda, toplam sayıları için örnekleme dengelemek için çarpılır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="0d1fc-108">Telemetri işlemcilerle filtreleme [ASP.NET](#filtering) veya [Java](app-insights-java-filter-telemetry.md) seçin veya sunucuya gönderilmeden önce SDK telemetri değiştirme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="0d1fc-109">Örneğin, robots istekleri hariç tutarak telemetri hacmi azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="0d1fc-110">Ancak filtreleme örnekleme daha trafiğini azaltmak için daha basit bir yaklaşım.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="0d1fc-111">Ne iletilen üzerinde daha fazla denetim sağlar, ancak tüm başarılı istek filtresi, örneğin, istatistikleri - etkiler farkında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="0d1fc-112">[Telemetri başlatıcıları Özellikler ekleme](#add-properties) telemetri standart modüllerden dahil uygulamanızın gönderilen telemetri için.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="0d1fc-113">Örneğin, hesaplanan değerler ekleyebilirsiniz; veya veri Portalı'nda filtrelemek için sürüm numaralarıyla.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="0d1fc-114">[SDK API'si](app-insights-api-custom-events-metrics.md) özel olayları ve ölçümleri göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="0d1fc-115">Başlamadan önce:</span><span class="sxs-lookup"><span data-stu-id="0d1fc-115">Before you start:</span></span>

* <span data-ttu-id="0d1fc-116">Application Insights yükleme [ASP.NET SDK](app-insights-asp-net.md) veya [Java için SDK](app-insights-java-get-started.md) uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="0d1fc-117">Filtreleme: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="0d1fc-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="0d1fc-118">Bu teknik ne dahil ya da telemetri akışına dışlanan üzerinden daha doğrudan denetim olanağı verir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="0d1fc-119">Örnekleme ile birlikte kullanın ya da ayrı olarak.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="0d1fc-120">Telemetri filtrelemek için bir telemetri işlemci yazma ve SDK'sı ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="0d1fc-121">Tüm telemetri işlemcinizin gider ve akıştan bırakma ya da özellikleri eklemek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="0d1fc-122">Bu, HTTP isteği Toplayıcı ve bağımlılık toplayıcısı gibi standart modüllerden telemetri yanı sıra, kendiniz yazmıştır telemetri içerir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="0d1fc-123">Örneğin, robots ya da başarılı bağımlılık çağrıları isteklerini hakkında telemetriyi filtre olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="0d1fc-124">SDK'dan gelen gönderilen telemetriyi filtreleme işlemciler kullanarak portalında gördüğünüz istatistikleri eğme ve ilgili öğeler izleyin zorlaştırır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="0d1fc-125">Bunun yerine, kullanmayı [örnekleme](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="0d1fc-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="0d1fc-126">Bir telemetri işlemci (C#) oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d1fc-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="0d1fc-127">Projenize Application Insights SDK'sı sürüm 2.0.0 olduğunu doğrulayın veya daha sonra.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="0d1fc-128">Visual Studio Çözüm Gezgini'nde projenize sağ tıklayın ve NuGet paketlerini Yönet'i seçin.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="0d1fc-129">NuGet Paket Yöneticisi'nde Microsoft.applicationınsights.Web denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="0d1fc-130">Bir filtre oluşturmak için ITelemetryProcessor uygulayın.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="0d1fc-131">Telemetri modülü, telemetri başlatıcı ve telemetri kanal gibi başka bir genişletilebilirlik noktası budur.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="0d1fc-132">Telemetri işlemciler işleme zinciri oluşturmak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="0d1fc-133">Telemetri işlemcisi örneği olduğunda, sonraki işlemciye zincirindeki bir bağlantı geçir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="0d1fc-134">Telemetri veri noktası için işlem yöntemi geçirildiğinde, çalışır ve sonraki Telemetri işlemci zincirinde çağırır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. <span data-ttu-id="0d1fc-135">Bu Applicationınsights.Config'de ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0d1fc-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="0d1fc-136">(Burada örnekleme filtre başlatma aynı bölüm budur.)</span><span class="sxs-lookup"><span data-stu-id="0d1fc-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="0d1fc-137">Sınıfınızda ortak adlandırılmış özellikleri sağlayarak .config dosyasından dize değerlerini geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="0d1fc-138">Tür adı ve kodda sınıf ve özellik adları .config dosyasına hiçbir özellik adlarını eşleştirmek için dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="0d1fc-139">.Config dosyası mevcut olmayan türe veya özelliğe başvuruyorsa, SDK'yı sessizce tüm telemetri göndermeyi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="0d1fc-140">**Alternatif olarak,** kod filtrede başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="0d1fc-141">Uygun başlatma sınıfında - örneğin AppStart Global.asax.cs içinde - zincirine işlemci ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0d1fc-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="0d1fc-142">Bu noktadan sonra oluşturulan TelemetryClients, işlemci kullanır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="0d1fc-143">Örnek filtreleri</span><span class="sxs-lookup"><span data-stu-id="0d1fc-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="0d1fc-144">Yapay istekleri</span><span class="sxs-lookup"><span data-stu-id="0d1fc-144">Synthetic requests</span></span>
<span data-ttu-id="0d1fc-145">Bot ve web testi filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-145">Filter out bots and web tests.</span></span> <span data-ttu-id="0d1fc-146">Ölçüm Gezgini yapay kaynaklarını filtre seçeneğini sağlamakla birlikte, bu seçenek SDK filtreleyerek trafiğini azaltır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="0d1fc-147">Başarısız kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0d1fc-147">Failed authentication</span></span>
<span data-ttu-id="0d1fc-148">"401" yanıt istekleri filtreler.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="0d1fc-149">Hızlı uzak bağımlılık çağrıları filtre</span><span class="sxs-lookup"><span data-stu-id="0d1fc-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="0d1fc-150">Yalnızca yavaş çağrılar tanılamak istiyorsanız, hızlı olanları filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="0d1fc-151">Bu portalda gördüğünüz istatistikleri eğme.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="0d1fc-152">Bağımlılık çağrıları tüm hataları varsa gibi bağımlılık grafik arar.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="0d1fc-153">Bağımlılık sorunlarını tanılama</span><span class="sxs-lookup"><span data-stu-id="0d1fc-153">Diagnose dependency issues</span></span>
<span data-ttu-id="0d1fc-154">[Bu blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) bağımlılıkları için otomatik olarak normal ping göndererek bağımlılık sorunları tanılamak için bir proje açıklar.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="0d1fc-155">Özellikleri ekleyin: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="0d1fc-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="0d1fc-156">Tüm telemetri ile gönderilen genel özelliklerini tanımlamak için telemetri başlatıcıları kullanın; ve standart telemetri modülleri seçili davranışını geçersiz kılmak için.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="0d1fc-157">Örneğin, Web Paketi için Application Insights telemetri HTTP istekleriyle ilgili toplar.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="0d1fc-158">Varsayılan olarak, bu yanıt kodu ile herhangi bir istek başarısız olarak işaretler > = 400.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="0d1fc-159">Ancak başarılı 400 Muamele etmek istiyorsanız, başarı özelliğini ayarlayan bir telemetri Başlatıcı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="0d1fc-160">Bir telemetri Başlatıcı sağladığınız adlı Track*() yöntemlerden herhangi birini zaman çağrılır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="0d1fc-161">Bu, standart telemetri modülleri tarafından adlı yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="0d1fc-162">Kurala göre bu modülleri başlatıcısı tarafından zaten ayarlanmış herhangi bir özelliği ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="0d1fc-163">**Başlatıcı tanımlayın**</span><span class="sxs-lookup"><span data-stu-id="0d1fc-163">**Define your initializer**</span></span>

<span data-ttu-id="0d1fc-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="0d1fc-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="0d1fc-165">**Başlatıcı yükleme**</span><span class="sxs-lookup"><span data-stu-id="0d1fc-165">**Load your initializer**</span></span>

<span data-ttu-id="0d1fc-166">Applicationınsights.Config'de:</span><span class="sxs-lookup"><span data-stu-id="0d1fc-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="0d1fc-167">*Alternatif olarak,* kodda, örneğin Global.aspx.cs Başlatıcı örneği:</span><span class="sxs-lookup"><span data-stu-id="0d1fc-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="0d1fc-168">Bu örnek daha fazla bilgi bakın.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="0d1fc-169">JavaScript telemetri başlatıcıları</span><span class="sxs-lookup"><span data-stu-id="0d1fc-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="0d1fc-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0d1fc-170">*JavaScript*</span></span>

<span data-ttu-id="0d1fc-171">Portaldan aldığınız başlatma koddan hemen sonra bir telemetri başlatıcı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0d1fc-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="0d1fc-172">TelemetryItem üzerinde kullanılabilir özel olmayan özelliklerin özeti için bkz: [uygulama Öngörüler dışarı veri modeli](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="0d1fc-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="0d1fc-173">İstediğiniz sayıda başlatıcıları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="0d1fc-174">ITelemetryProcessor ve ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="0d1fc-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="0d1fc-175">Telemetri işlemciler ve telemetri başlatıcıları arasındaki fark nedir?</span><span class="sxs-lookup"><span data-stu-id="0d1fc-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="0d1fc-176">Bazı üst üste geliyor bunlarla yapabileceklerinizi içinde vardır: her ikisi de telemetri özellikleri eklemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="0d1fc-177">TelemetryInitializers TelemetryProcessors önce her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="0d1fc-178">TelemetryProcessors tamamen değiştirin veya bir telemetri öğesi atmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="0d1fc-179">TelemetryProcessors performans sayacı telemetri işlem yok.</span><span class="sxs-lookup"><span data-stu-id="0d1fc-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="0d1fc-180">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="0d1fc-180">Reference docs</span></span>
* [<span data-ttu-id="0d1fc-181">API’ye Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0d1fc-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="0d1fc-182">ASP.NET başvurusu</span><span class="sxs-lookup"><span data-stu-id="0d1fc-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="0d1fc-183">SDK kod</span><span class="sxs-lookup"><span data-stu-id="0d1fc-183">SDK Code</span></span>
* [<span data-ttu-id="0d1fc-184">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="0d1fc-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="0d1fc-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="0d1fc-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="0d1fc-186">JavaScript SDK'sı</span><span class="sxs-lookup"><span data-stu-id="0d1fc-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="0d1fc-187"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d1fc-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="0d1fc-188">Arama olayları ve günlükleri</span><span class="sxs-lookup"><span data-stu-id="0d1fc-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="0d1fc-189">Örnekleme</span><span class="sxs-lookup"><span data-stu-id="0d1fc-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="0d1fc-190">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0d1fc-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
