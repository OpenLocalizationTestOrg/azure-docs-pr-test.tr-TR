---
title: "aaaAzure Service Fabric uygulama düzeyi izleme | Microsoft Docs"
description: "Uygulama hakkında bilgi edinin ve hizmet düzeyi olayları ve günlükleri toomonitor kullanılan ve Azure Service Fabric kümeleri tanılayın."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="1e624-103">Uygulama ve hizmet düzeyi olay ve günlük oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e624-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="1e624-104">Özel olaylar Hello koduyla düzenleme</span><span class="sxs-lookup"><span data-stu-id="1e624-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="1e624-105">Merhaba kod düzenleme hello çoğu diğer yönlerini hizmetlerinizi izleme temelini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1e624-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="1e624-106">İzleme, bir şeyler yanlış ve toodiagnose ne sabit toobe gerektiğini biliyor hello tek yoludur.</span><span class="sxs-lookup"><span data-stu-id="1e624-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="1e624-107">Teknik olarak olası tooconnect bir hata ayıklayıcı tooa üretim hizmeti olmasına rağmen ortak bir uygulama değildir.</span><span class="sxs-lookup"><span data-stu-id="1e624-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="1e624-108">Bu nedenle, izleme verileri ayrıntılı önemlidir.</span><span class="sxs-lookup"><span data-stu-id="1e624-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="1e624-109">Bazı ürünler kodunuzu otomatik olarak işaretleme.</span><span class="sxs-lookup"><span data-stu-id="1e624-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="1e624-110">Bu çözüm de olsa da, el ile araçları neredeyse her zaman gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1e624-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="1e624-111">Merhaba bitimine hello uygulamanızın hatalarını ayıklama yeterli bilgi tooforensically olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e624-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="1e624-112">Bu belge, kodunuzu farklı yaklaşımlara tooinstrumenting açıklar ve ne zaman toochoose bir yaklaşımını başka bir.</span><span class="sxs-lookup"><span data-stu-id="1e624-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="1e624-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="1e624-113">EventSource</span></span>
<span data-ttu-id="1e624-114">Visual Studio'da bir şablondan bir Service Fabric çözüm oluşturduğunuzda bir **EventSource**-türetilen sınıfı (**ServiceEventSource** veya **ActorEventSource**) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1e624-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="1e624-115">Bir şablon oluşturduğunuzu, uygulama veya hizmet için olayları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e624-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="1e624-116">Merhaba **EventSource** adı **gerekir** benzersiz olmalı ve hello varsayılan şablon dizeden Şirketim - adlandırılmamalıdır&lt;çözüm&gt; - &lt; Proje&gt;.</span><span class="sxs-lookup"><span data-stu-id="1e624-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="1e624-117">Birden çok sahip **EventSource** kullanan tanımları hello bir sorununu çalışma zamanında aynı adı neden olur.</span><span class="sxs-lookup"><span data-stu-id="1e624-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="1e624-118">Her tanımlanan olay benzersiz bir tanımlayıcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e624-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="1e624-119">Tanımlayıcı benzersiz değilse, bir çalışma zamanı hatası oluşur.</span><span class="sxs-lookup"><span data-stu-id="1e624-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="1e624-120">Bazı kuruluşlar ayrı geliştirme ekipleri arasında tanımlayıcıları tooavoid çakışmalar için değerleri aralığı preassign.</span><span class="sxs-lookup"><span data-stu-id="1e624-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="1e624-121">Daha fazla bilgi için bkz: [Vance'nın blogu](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) veya hello [MSDN belgelerine](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="1e624-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="1e624-122">Yapılandırılmış EventSource olaylarını kullanma</span><span class="sxs-lookup"><span data-stu-id="1e624-122">Using structured EventSource events</span></span>

<span data-ttu-id="1e624-123">Bu bölümdeki hello kod örneklerde hello olayların her biri tanımlanmış için belirli bir durumda, örneğin, bir hizmet türünün kaydedildiğinde.</span><span class="sxs-lookup"><span data-stu-id="1e624-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="1e624-124">Kullanım örneği tarafından iletileri tanımlamak, veri hello hata hello metinle paketlenmesi ve şunları yapabilirsiniz daha kolayca arama ve filtre hello adları veya hello değerlerini temel alarak özellikleri belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="1e624-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="1e624-125">Hello araç çıktısının yapılandırılması daha kolay tooconsume kolaylaştırır, ancak daha fazla düşünce gerektirir ve her kullanım örneği için yeni bir olay toodefine saat.</span><span class="sxs-lookup"><span data-stu-id="1e624-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="1e624-126">Bazı olay tanımları hello tüm uygulama arasında paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="1e624-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="1e624-127">Örneğin, bir yöntemi Başlat veya Durdur için olay uygulama içinde birçok hizmetlerde yeniden.</span><span class="sxs-lookup"><span data-stu-id="1e624-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="1e624-128">Bir sipariş sistemi gibi bir etki alanına özgü hizmet olabilir bir **CreateOrder** kendi benzersiz olayın olay.</span><span class="sxs-lookup"><span data-stu-id="1e624-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="1e624-129">Bu yaklaşım birçok olayları oluşturmak ve potansiyel olarak tanımlayıcıları proje ekipleri arasında gerektiren.</span><span class="sxs-lookup"><span data-stu-id="1e624-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="1e624-130">EventSource genel kullanma</span><span class="sxs-lookup"><span data-stu-id="1e624-130">Using EventSource generically</span></span>

<span data-ttu-id="1e624-131">Belirli olayları tanımlama zor olabilir çünkü çoğu kişi genellikle dize olarak kendi bilgilerini çıktı parametreleri ortak bir dizi birkaç olaylarla tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="1e624-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="1e624-132">Yapılandırılmış hello en boy çoğunu kaybolur ve daha zor toosearch ve filtre hello sonuçları değil.</span><span class="sxs-lookup"><span data-stu-id="1e624-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="1e624-133">Bu yaklaşımda, genellikle toohello günlük düzeylerini karşılık birkaç olaylar tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="1e624-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="1e624-134">Aşağıdaki kod parçacığında hello hata ayıklama ve hata iletisini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="1e624-134">hello following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

<span data-ttu-id="1e624-135">Karma yapılandırılmış ve genel araçları kullanarak da iyi çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="1e624-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="1e624-136">Yapılandırılmış araçları hataları ve ölçümleri raporlama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e624-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="1e624-137">Genel olaylar ayrıntılı hello için kullanılabilir diğer bir deyişle oturum tüketilen mühendisleri tarafından sorun giderme için.</span><span class="sxs-lookup"><span data-stu-id="1e624-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="1e624-138">ASP.NET oturum çekirdek</span><span class="sxs-lookup"><span data-stu-id="1e624-138">ASP.NET Core logging</span></span>

<span data-ttu-id="1e624-139">Buna ait önemli toocarefully planlama kodunuzu nasıl izleme.</span><span class="sxs-lookup"><span data-stu-id="1e624-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="1e624-140">Merhaba sağ araçları planı büyük olasılıkla kodunuzu temel destabilizing ve tooreinstrument hello kod ihtiyaç duyan önlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e624-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="1e624-141">tooreduce risk gibi bir araç kitaplığı seçebilirsiniz [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), Microsoft ASP.NET Core parçası olduğu.</span><span class="sxs-lookup"><span data-stu-id="1e624-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="1e624-142">ASP.NET Core sahip bir [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) var olan kodu hello etkisini en aza indirerek tercih ettiğiniz hello sağlayıcı ile kullanabileceğiniz arabirimi.</span><span class="sxs-lookup"><span data-stu-id="1e624-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="1e624-143">Windows ve Linux üzerinde ASP.NET Core hello kodu kullanın ve araçları kodunuzu standartlaştırılmış şekilde hello .NET Framework tam.</span><span class="sxs-lookup"><span data-stu-id="1e624-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="1e624-144">Bu daha aşağıda incelediniz:</span><span class="sxs-lookup"><span data-stu-id="1e624-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="1e624-145">Service Fabric Microsoft.Extensions.Logging kullanma</span><span class="sxs-lookup"><span data-stu-id="1e624-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="1e624-146">Merhaba tooinstrument istediğiniz Microsoft.Extensions.Logging NuGet paketi toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e624-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="1e624-147">Ayrıca, herhangi bir sağlayıcı paket ekleme (üçüncü taraf paketi için aşağıdaki örneğine hello bakın).</span><span class="sxs-lookup"><span data-stu-id="1e624-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="1e624-148">Daha fazla bilgi için bkz: [ASP.NET çekirdek günlüğü](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="1e624-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="1e624-149">Ekleme bir **kullanarak** Microsoft.Extensions.Logging tooyour hizmet dosyası için yönerge.</span><span class="sxs-lookup"><span data-stu-id="1e624-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="1e624-150">Hizmet sınıfınızı içinde özel bir değişken tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="1e624-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="1e624-151">Hizmet sınıfınızı Hello oluşturucuda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e624-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="1e624-152">Yöntemlerinizi kodunuzda izleme başlatın.</span><span class="sxs-lookup"><span data-stu-id="1e624-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="1e624-153">Bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1e624-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="1e624-154">Diğer günlük sağlayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="1e624-154">Using other logging providers</span></span>

<span data-ttu-id="1e624-155">Bazı üçüncü taraf sağlayıcılar hello önceki bölümünde açıklanan hello yaklaşımı kullanmak da dahil olmak üzere [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), ve [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="1e624-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="1e624-156">Her birinde ASP.NET oturum çekirdek içine takın veya ayrı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e624-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="1e624-157">Serilog Günlükçü gönderilen tüm iletiler aşağıdakilere zenginleştirir bir özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="1e624-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="1e624-158">Bu özellik kullanışlı toooutput hello hizmet adını, türünü ve bölüm bilgileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e624-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="1e624-159">toouse bu özelliği hello ASP.NET Core altyapı de şu adımları yapın:</span><span class="sxs-lookup"><span data-stu-id="1e624-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="1e624-160">Serilog, Serilog.Extensions.Logging, hello ve toohello proje Serilog.Sinks.Observable NuGet paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e624-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="1e624-161">Merhaba sonraki örnekte, ayrıca Serilog.Sinks.Literate ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e624-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="1e624-162">Daha iyi bir yaklaşım, bu makalenin sonraki bölümlerinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1e624-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="1e624-163">Serilog içinde LoggerConfiguration ve hello Günlükçü örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e624-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="1e624-164">Bir Serilog.ILogger bağımsız değişkeni toohello hizmet oluşturucu ekleyin ve Günlükçü yeni oluşturulan hello geçirin.</span><span class="sxs-lookup"><span data-stu-id="1e624-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="1e624-165">Merhaba hizmet oluşturucuda hello hello özelliği enrichers oluşturur kod aşağıdaki hello eklemek **ServiceTypeName**, **ServiceName**, **PartitionID**ve  **InstanceId** hello hizmetinin özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="1e624-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="1e624-166">Kodunuzda Microsoft.Extensions.Logging.ILogger kullanabilmeniz için ayrıca bir özelliği enricher toohello ASP.NET Core günlük Fabrika ekler.</span><span class="sxs-lookup"><span data-stu-id="1e624-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. <span data-ttu-id="1e624-167">Gereç hello kod hello aynı ASP.NET Core Serilog olmadan kullanıyormuş gibi.</span><span class="sxs-lookup"><span data-stu-id="1e624-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="1e624-168">Merhaba statik kullanmamanızı öneririz Log.Logger örnek önceki hello ile.</span><span class="sxs-lookup"><span data-stu-id="1e624-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="1e624-169">Service Fabric birden çok ana bilgisayar aynı hizmeti Merhaba tek bir işlem içinde türü.</span><span class="sxs-lookup"><span data-stu-id="1e624-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="1e624-170">Kullanırsanız, statik Log.Logger Merhaba, hello özelliği enrichers hello son yazan çalışan tüm örnekleri için değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e624-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="1e624-171">Bu neden hello _logger değişkeni hello hizmet sınıfı bir özel üye değişkeni nedenlerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="1e624-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="1e624-172">Ayrıca, hizmetleri kullanılan hello _logger kullanılabilir toocommon kod yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e624-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="1e624-173">Oturum açma sağlayıcısı seçme</span><span class="sxs-lookup"><span data-stu-id="1e624-173">Choosing a logging provider</span></span>

<span data-ttu-id="1e624-174">Uygulamanızı yüksek performans üzerinde dayalıysa **EventSource** genellikle iyi bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="1e624-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="1e624-175">**EventSource** *genellikle* daha az kaynak kullanır ve ASP.NET Core günlüğü ya da herhangi bir hello kullanılabilir üçüncü taraf çözümleri daha iyi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e624-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="1e624-176">Bu hizmet performans kullanarak dayalı olup olmadığını ancak birçok Hizmetleri için bir sorun değildir **EventSource** daha iyi bir seçim olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e624-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="1e624-177">Ancak, günlük, tooget bu yararları yapılandırılmış **EventSource** mühendislik ekibi daha büyük bir yatırım gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1e624-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="1e624-178">Mümkünse, birkaç günlüğe kaydetme seçeneklerini hızlı prototipi yapın ve ardından hello gereksinimlerinizi en iyi karşılayan bir tane seçin.</span><span class="sxs-lookup"><span data-stu-id="1e624-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e624-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e624-179">Next steps</span></span>

<span data-ttu-id="1e624-180">Uygulamalar ve hizmetler günlüğü sağlayıcısı tooinstrument seçtikten sonra günlüklerini ve olayları tooany analiz platformu gönderilmeden önce bir araya getirilir toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e624-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="1e624-181">Hakkında bilgi edinin [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) ve [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter bazı seçenekleri önerilen hello anlama.</span><span class="sxs-lookup"><span data-stu-id="1e624-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
