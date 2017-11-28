---
title: "aaaFiltering ve içinde ön işleme hello Azure Application Insights SDK'sı | Microsoft Docs"
description: "Telemetri işlemciler ve Telemetri başlatıcıları hello SDK toofilter için yazma veya hello telemetri toohello Application Insights portalındaki gönderilmeden önce özellikleri toohello veri ekleyin."
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
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="eab75-103">Filtreleme ve hello Application Insights SDK'sı telemetri ön işleme</span><span class="sxs-lookup"><span data-stu-id="eab75-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="eab75-104">Yazma ve eklentiler nasıl telemetri yakalanan ve toohello Application Insights hizmeti gönderilmeden önce işlenen hello Application Insights SDK'sı toocustomize için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eab75-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="eab75-105">[Örnekleme](app-insights-sampling.md) , istatistikleri etkilemeden telemetri hello hacmini azaltır.</span><span class="sxs-lookup"><span data-stu-id="eab75-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="eab75-106">Birlikte tutar ilgili veri noktaları aralarında bir sorunu tanılamada gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab75-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="eab75-107">Merhaba Portalı'nda hello örnekleme için çarpılan toocompensate hello toplam sayı olan.</span><span class="sxs-lookup"><span data-stu-id="eab75-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="eab75-108">Telemetri işlemcilerle filtreleme [ASP.NET](#filtering) veya [Java](app-insights-java-filter-telemetry.md) seçin veya toohello sunucu gönderilmeden önce hello SDK telemetri değiştirme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="eab75-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="eab75-109">Örneğin, robots istekleri hariç tutarak telemetri hello hacmi azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="eab75-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="eab75-110">Ancak filtreleme örnekleme daha fazla temel bir yaklaşım tooreducing trafiği.</span><span class="sxs-lookup"><span data-stu-id="eab75-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="eab75-111">Ne iletilen üzerinde daha fazla denetim sağlar, ancak tüm başarılı istek filtresi toobe Bu, istatistikleri - Örneğin, etkiler farkında olması.</span><span class="sxs-lookup"><span data-stu-id="eab75-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="eab75-112">[Telemetri başlatıcıları Özellikler ekleme](#add-properties) telemetri hello standart modüllerden dahil uygulamanızın gönderilen tooany telemetri.</span><span class="sxs-lookup"><span data-stu-id="eab75-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="eab75-113">Örneğin, hesaplanan değerler ekleyebilirsiniz; veya toofilter hello veri hello Portalı'nda sürüm numaralarıyla.</span><span class="sxs-lookup"><span data-stu-id="eab75-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="eab75-114">[Merhaba SDK API'si](app-insights-api-custom-events-metrics.md) kullanılan toosend özel olayları ve ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="eab75-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="eab75-115">Başlamadan önce:</span><span class="sxs-lookup"><span data-stu-id="eab75-115">Before you start:</span></span>

* <span data-ttu-id="eab75-116">Merhaba Application Insights yükleme [ASP.NET SDK](app-insights-asp-net.md) veya [Java için SDK](app-insights-java-get-started.md) uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="eab75-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="eab75-117">Filtreleme: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="eab75-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="eab75-118">Bu teknik ne dahil ya da hello telemetri akışına dışlanan üzerinden daha doğrudan denetim olanağı verir.</span><span class="sxs-lookup"><span data-stu-id="eab75-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="eab75-119">Örnekleme ile birlikte kullanın ya da ayrı olarak.</span><span class="sxs-lookup"><span data-stu-id="eab75-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="eab75-120">telemetri işlemci yazma ve hello SDK ile kaydetmek toofilter telemetri.</span><span class="sxs-lookup"><span data-stu-id="eab75-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="eab75-121">Tüm telemetri işlemcinizin gider ve toodrop seçebilirsiniz hello ondan akışla aktarmak veya özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eab75-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="eab75-122">Bu, telemetri hello HTTP isteği Toplayıcı ve hello bağımlılık Toplayıcı gibi hello standart modüllerden yanı sıra, kendiniz yazmıştır telemetri içerir.</span><span class="sxs-lookup"><span data-stu-id="eab75-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="eab75-123">Örneğin, robots ya da başarılı bağımlılık çağrıları isteklerini hakkında telemetriyi filtre olabilir.</span><span class="sxs-lookup"><span data-stu-id="eab75-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="eab75-124">SDK Hello gönderilen hello telemetri filtreleme işlemcileri kullanan eğme hello portalında görebilir ve zor toofollow olun hello istatistikleri ilgili öğeleri.</span><span class="sxs-lookup"><span data-stu-id="eab75-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="eab75-125">Bunun yerine, kullanmayı [örnekleme](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="eab75-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="eab75-126">Bir telemetri işlemci (C#) oluşturma</span><span class="sxs-lookup"><span data-stu-id="eab75-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="eab75-127">Projenizi bu hello Application Insights SDK'sı sürüm 2.0.0 olduğunu doğrulayın veya daha sonra.</span><span class="sxs-lookup"><span data-stu-id="eab75-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="eab75-128">Visual Studio Çözüm Gezgini'nde projenize sağ tıklayın ve NuGet paketlerini Yönet'i seçin.</span><span class="sxs-lookup"><span data-stu-id="eab75-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="eab75-129">NuGet Paket Yöneticisi'nde Microsoft.applicationınsights.Web denetleyin.</span><span class="sxs-lookup"><span data-stu-id="eab75-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="eab75-130">toocreate bir filtre ITelemetryProcessor uygulayın.</span><span class="sxs-lookup"><span data-stu-id="eab75-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="eab75-131">Telemetri modülü, telemetri başlatıcı ve telemetri kanal gibi başka bir genişletilebilirlik noktası budur.</span><span class="sxs-lookup"><span data-stu-id="eab75-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="eab75-132">Telemetri işlemciler işleme zinciri oluşturmak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="eab75-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="eab75-133">Telemetri işlemcisi örneği olduğunda, bir bağlantı toohello sonraki işlemci hello zincirinde geçir.</span><span class="sxs-lookup"><span data-stu-id="eab75-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="eab75-134">Telemetri veri noktası toohello işlem yöntemi geçirildiğinde çalışmasını yapar ve sonra çağrıları hello zincirinde sonraki Telemetri işlemci hello.</span><span class="sxs-lookup"><span data-stu-id="eab75-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
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
1. <span data-ttu-id="eab75-135">Bu Applicationınsights.Config'de ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eab75-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="eab75-136">(Merhaba budur başlatma burada örnekleme filtre aynı bölüm.)</span><span class="sxs-lookup"><span data-stu-id="eab75-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="eab75-137">Sınıfınızda ortak adlandırılmış özellikleri sağlayarak hello .config dosyasından dize değerlerini geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab75-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="eab75-138">Toomatch hello türü adını herhangi hello .config dosyası toohello sınıfı özellik adlarını ve özellik adları hello kodda dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="eab75-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="eab75-139">Merhaba .config dosyası mevcut olmayan türe veya özelliğe başvuruyorsa, hello SDK sessizce toosend tüm telemetri başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="eab75-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="eab75-140">**Alternatif olarak,** hello filtre kodda başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab75-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="eab75-141">Uygun başlatma sınıfında - örneğin AppStart Global.asax.cs içinde - hello zincirine işlemci ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eab75-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="eab75-142">Bu noktadan sonra oluşturulan TelemetryClients, işlemci kullanır.</span><span class="sxs-lookup"><span data-stu-id="eab75-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="eab75-143">Örnek filtreleri</span><span class="sxs-lookup"><span data-stu-id="eab75-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="eab75-144">Yapay istekleri</span><span class="sxs-lookup"><span data-stu-id="eab75-144">Synthetic requests</span></span>
<span data-ttu-id="eab75-145">Bot ve web testi filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="eab75-145">Filter out bots and web tests.</span></span> <span data-ttu-id="eab75-146">Ölçüm Gezgini sağlamakla birlikte seçeneği toofilter yapay kaynakları çıkışı Merhaba, bu seçenek SDK hello filtreleyerek trafiğini azaltır.</span><span class="sxs-lookup"><span data-stu-id="eab75-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="eab75-147">Başarısız kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="eab75-147">Failed authentication</span></span>
<span data-ttu-id="eab75-148">"401" yanıt istekleri filtreler.</span><span class="sxs-lookup"><span data-stu-id="eab75-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="eab75-149">Hızlı uzak bağımlılık çağrıları filtre</span><span class="sxs-lookup"><span data-stu-id="eab75-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="eab75-150">Yavaş toodiagnose çağrıları yalnızca istiyorsanız hello hızlı olanları filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="eab75-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="eab75-151">Bu hello portalında gördüğünüz hello istatistikleri eğme.</span><span class="sxs-lookup"><span data-stu-id="eab75-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="eab75-152">Merhaba bağımlılık çağrıları tüm hataları varsa gibi hello bağımlılık grafik arar.</span><span class="sxs-lookup"><span data-stu-id="eab75-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="eab75-153">Bağımlılık sorunlarını tanılama</span><span class="sxs-lookup"><span data-stu-id="eab75-153">Diagnose dependency issues</span></span>
<span data-ttu-id="eab75-154">[Bu blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) otomatik olarak normal ping toodependencies göndererek proje toodiagnose bağımlılık sorunları açıklar.</span><span class="sxs-lookup"><span data-stu-id="eab75-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="eab75-155">Özellikleri ekleyin: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="eab75-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="eab75-156">Gönderilen telemetri başlatıcıları toodefine genel özellikleri ile tüm telemetri kullanın; ve hello standart telemetri modülleri davranışını toooverride seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="eab75-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="eab75-157">Örneğin, Web Paketi için Application Insights hello HTTP istekleriyle ilgili telemetri toplar.</span><span class="sxs-lookup"><span data-stu-id="eab75-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="eab75-158">Varsayılan olarak, bu yanıt kodu ile herhangi bir istek başarısız olarak işaretler > = 400.</span><span class="sxs-lookup"><span data-stu-id="eab75-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="eab75-159">Ancak, başarı olarak tootreat 400 istiyorsanız, hello başarı özelliğini ayarlayan bir telemetri Başlatıcı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="eab75-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="eab75-160">Bir telemetri Başlatıcı sağlarsanız, herhangi bir Track*() hello olduğunda çağrılır yöntemleri çağrılır.</span><span class="sxs-lookup"><span data-stu-id="eab75-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="eab75-161">Bu hello standart telemetri modülleri tarafından adlı yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="eab75-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="eab75-162">Kurala göre bu modülleri başlatıcısı tarafından zaten ayarlanmış herhangi bir özelliği ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="eab75-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="eab75-163">**Başlatıcı tanımlayın**</span><span class="sxs-lookup"><span data-stu-id="eab75-163">**Define your initializer**</span></span>

<span data-ttu-id="eab75-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="eab75-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
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
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

<span data-ttu-id="eab75-165">**Başlatıcı yükleme**</span><span class="sxs-lookup"><span data-stu-id="eab75-165">**Load your initializer**</span></span>

<span data-ttu-id="eab75-166">Applicationınsights.Config'de:</span><span class="sxs-lookup"><span data-stu-id="eab75-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="eab75-167">*Alternatif olarak,* kodda, örneğin Global.aspx.cs hello Başlatıcı örneği:</span><span class="sxs-lookup"><span data-stu-id="eab75-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="eab75-168">Bu örnek daha fazla bilgi bakın.</span><span class="sxs-lookup"><span data-stu-id="eab75-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="eab75-169">JavaScript telemetri başlatıcıları</span><span class="sxs-lookup"><span data-stu-id="eab75-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="eab75-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="eab75-170">*JavaScript*</span></span>

<span data-ttu-id="eab75-171">Merhaba portalından aldığınız hemen hello başlatma koddan sonra bir telemetri başlatıcı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eab75-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="eab75-172">Merhaba özel olmayan özellikleri hello telemetryItem üzerinde kullanılabilir özeti için bkz: [uygulama Öngörüler dışarı veri modeli](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="eab75-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="eab75-173">İstediğiniz sayıda başlatıcıları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab75-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="eab75-174">ITelemetryProcessor ve ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="eab75-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="eab75-175">Merhaba telemetri işlemciler ve telemetri başlatıcıları arasındaki fark nedir?</span><span class="sxs-lookup"><span data-stu-id="eab75-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="eab75-176">Bazı üst üste geliyor bunlarla yapabileceklerinizi içinde vardır: her ikisi de kullanılan tooadd özellikleri tootelemetry olabilir.</span><span class="sxs-lookup"><span data-stu-id="eab75-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="eab75-177">TelemetryInitializers TelemetryProcessors önce her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="eab75-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="eab75-178">TelemetryProcessors toocompletely Değiştir izin ver veya bir telemetri öğesini atın.</span><span class="sxs-lookup"><span data-stu-id="eab75-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="eab75-179">TelemetryProcessors performans sayacı telemetri işlem yok.</span><span class="sxs-lookup"><span data-stu-id="eab75-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="eab75-180">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="eab75-180">Reference docs</span></span>
* [<span data-ttu-id="eab75-181">API’ye Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="eab75-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="eab75-182">ASP.NET başvurusu</span><span class="sxs-lookup"><span data-stu-id="eab75-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="eab75-183">SDK kod</span><span class="sxs-lookup"><span data-stu-id="eab75-183">SDK Code</span></span>
* [<span data-ttu-id="eab75-184">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="eab75-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="eab75-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="eab75-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="eab75-186">JavaScript SDK'sı</span><span class="sxs-lookup"><span data-stu-id="eab75-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="eab75-187"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eab75-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="eab75-188">Arama olayları ve günlükleri</span><span class="sxs-lookup"><span data-stu-id="eab75-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="eab75-189">Örnekleme</span><span class="sxs-lookup"><span data-stu-id="eab75-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="eab75-190">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="eab75-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
