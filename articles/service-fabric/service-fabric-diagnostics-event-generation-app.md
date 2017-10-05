---
title: "Azure Service Fabric uygulama düzeyinde izleme | Microsoft Docs"
description: "Uygulama ve hizmet düzeyi olayları ve günlükleri izlemek ve Azure Service Fabric kümeleri tanılamak için kullanılan hakkında bilgi edinin."
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
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="02856-103">Uygulama ve hizmet düzeyi olay ve günlük oluşturma</span><span class="sxs-lookup"><span data-stu-id="02856-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="02856-104">Özel olaylar koduyla düzenleme</span><span class="sxs-lookup"><span data-stu-id="02856-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="02856-105">Kod işaretleme çoğu diğer yönlerini hizmetlerinizi izleme temelidir.</span><span class="sxs-lookup"><span data-stu-id="02856-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="02856-106">İzleme bildiğiniz bir şeylerin yanlış olduğunu tek yoludur ve neyi düzeltilmesi gerektiğini tanılamak için.</span><span class="sxs-lookup"><span data-stu-id="02856-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="02856-107">Teknik olarak, bir hata ayıklayıcısı bir üretim hizmetine bağlanmak mümkün olsa da, ortak bir uygulama değildir.</span><span class="sxs-lookup"><span data-stu-id="02856-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="02856-108">Bu nedenle, izleme verileri ayrıntılı önemlidir.</span><span class="sxs-lookup"><span data-stu-id="02856-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="02856-109">Bazı ürünler kodunuzu otomatik olarak işaretleme.</span><span class="sxs-lookup"><span data-stu-id="02856-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="02856-110">Bu çözüm de olsa da, el ile araçları neredeyse her zaman gereklidir.</span><span class="sxs-lookup"><span data-stu-id="02856-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="02856-111">Sonunda forensically uygulamada hata ayıklama için yeterli bilgiye sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="02856-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="02856-112">Bu belgede, kodunuz ve ne zaman bir yaklaşım başka bir ad seçin düzenleme için farklı yaklaşımlara açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="02856-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="02856-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="02856-113">EventSource</span></span>
<span data-ttu-id="02856-114">Visual Studio'da bir şablondan bir Service Fabric çözüm oluşturduğunuzda bir **EventSource**-türetilen sınıfı (**ServiceEventSource** veya **ActorEventSource**) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="02856-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="02856-115">Bir şablon oluşturduğunuzu, uygulama veya hizmet için olayları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02856-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="02856-116">**EventSource** adı **gerekir** benzersiz olmalı ve varsayılan şablon dizeden Şirketim - adlandırılmamalıdır&lt;çözüm&gt;-&lt;proje&gt;.</span><span class="sxs-lookup"><span data-stu-id="02856-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="02856-117">Birden çok sahip **EventSource** aynı adı kullanan tanımları çalışma zamanında bir sorunu neden olur.</span><span class="sxs-lookup"><span data-stu-id="02856-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="02856-118">Her tanımlanan olay benzersiz bir tanımlayıcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="02856-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="02856-119">Tanımlayıcı benzersiz değilse, bir çalışma zamanı hatası oluşur.</span><span class="sxs-lookup"><span data-stu-id="02856-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="02856-120">Bazı kuruluşlar ayrı geliştirme ekipleri arasındaki çakışmaları önleme tanımlayıcıları için değerlerin aralıkları preassign.</span><span class="sxs-lookup"><span data-stu-id="02856-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="02856-121">Daha fazla bilgi için bkz: [Vance'nın blogu](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) veya [MSDN belgelerine](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="02856-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="02856-122">Yapılandırılmış EventSource olaylarını kullanma</span><span class="sxs-lookup"><span data-stu-id="02856-122">Using structured EventSource events</span></span>

<span data-ttu-id="02856-123">Bu bölümdeki kod örnekleri, olayların her biri tanımlanmış bir belirli durumlarda, örneğin, bir hizmet türünün kaydedildiğinde.</span><span class="sxs-lookup"><span data-stu-id="02856-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="02856-124">Kullanım örneği tarafından iletileri tanımlamak, veri hata metni ile paketlenmesi ve daha yapabilecekleriniz kolayca arama ve filtre adları veya belirtilen özelliklerin değerlerine göre.</span><span class="sxs-lookup"><span data-stu-id="02856-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="02856-125">İzleme çıkışı yapar yapılandırılması kullanmak, daha kolay ancak gerektiriyor her kullanım durumu için yeni bir olayı tanımlamak için daha fazla düşünce ve saati.</span><span class="sxs-lookup"><span data-stu-id="02856-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="02856-126">Bazı olay tanımları tüm uygulama arasında paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="02856-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="02856-127">Örneğin, bir yöntemi Başlat veya Durdur için olay uygulama içinde birçok hizmetlerde yeniden.</span><span class="sxs-lookup"><span data-stu-id="02856-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="02856-128">Bir sipariş sistemi gibi bir etki alanına özgü hizmet olabilir bir **CreateOrder** kendi benzersiz olayın olay.</span><span class="sxs-lookup"><span data-stu-id="02856-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="02856-129">Bu yaklaşım birçok olayları oluşturmak ve potansiyel olarak tanımlayıcıları proje ekipleri arasında gerektiren.</span><span class="sxs-lookup"><span data-stu-id="02856-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="02856-130">EventSource genel kullanma</span><span class="sxs-lookup"><span data-stu-id="02856-130">Using EventSource generically</span></span>

<span data-ttu-id="02856-131">Belirli olayları tanımlama zor olabilir çünkü çoğu kişi genellikle dize olarak kendi bilgilerini çıktı parametreleri ortak bir dizi birkaç olaylarla tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="02856-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="02856-132">Yapılandırılmış en boy çoğunu kaybolur ve aramak ve sonuçları filtrelemek daha zordur.</span><span class="sxs-lookup"><span data-stu-id="02856-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="02856-133">Bu yaklaşımda, genellikle günlük düzeylerini karşılık birkaç olaylar tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="02856-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="02856-134">Aşağıdaki kod parçacığında, bir hata ayıklama ve hata iletisi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="02856-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
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

<span data-ttu-id="02856-135">Karma yapılandırılmış ve genel araçları kullanarak da iyi çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="02856-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="02856-136">Yapılandırılmış araçları hataları ve ölçümleri raporlama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="02856-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="02856-137">Genel olaylar, sorun giderme için mühendisleri tarafından kullanılan ayrıntılı günlük kaydı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="02856-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="02856-138">ASP.NET oturum çekirdek</span><span class="sxs-lookup"><span data-stu-id="02856-138">ASP.NET Core logging</span></span>

<span data-ttu-id="02856-139">Kodunuzu nasıl izleme dikkatle planlamanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="02856-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="02856-140">Sağ araçları planı büyük olasılıkla kod temeliniz destabilizing ve kod reinstrument gerek önlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="02856-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="02856-141">Riskini azaltmak için bir araç kitaplığı gibi seçebilirsiniz [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), Microsoft ASP.NET Core parçası olduğu.</span><span class="sxs-lookup"><span data-stu-id="02856-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="02856-142">ASP.NET Core sahip bir [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) var olan kodu üzerindeki etkisini en aza indirerek tercih ettiğiniz sağlayıcısı ile birlikte kullanabileceğiniz arabirimi.</span><span class="sxs-lookup"><span data-stu-id="02856-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="02856-143">Windows ve Linux üzerinde ASP.NET Core kodu kullanabilirsiniz ve tam .NET Framework, bu nedenle araçları kodunuzu standartlaştırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="02856-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="02856-144">Bu daha aşağıda incelediniz:</span><span class="sxs-lookup"><span data-stu-id="02856-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="02856-145">Service Fabric Microsoft.Extensions.Logging kullanma</span><span class="sxs-lookup"><span data-stu-id="02856-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="02856-146">İstediğiniz projesine Microsoft.Extensions.Logging NuGet paketi ekleme aracı.</span><span class="sxs-lookup"><span data-stu-id="02856-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="02856-147">Ayrıca, herhangi bir sağlayıcı paket ekleme (üçüncü taraf paketi için aşağıdaki örneğe bakın).</span><span class="sxs-lookup"><span data-stu-id="02856-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="02856-148">Daha fazla bilgi için bkz: [ASP.NET çekirdek günlüğü](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="02856-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="02856-149">Ekleme bir **kullanarak** hizmet dosyanıza Microsoft.Extensions.Logging için yönerge.</span><span class="sxs-lookup"><span data-stu-id="02856-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="02856-150">Hizmet sınıfınızı içinde özel bir değişken tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="02856-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="02856-151">Hizmet sınıfınızı oluşturucuda bu kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="02856-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="02856-152">Yöntemlerinizi kodunuzda izleme başlatın.</span><span class="sxs-lookup"><span data-stu-id="02856-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="02856-153">Bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="02856-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="02856-154">Diğer günlük sağlayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="02856-154">Using other logging providers</span></span>

<span data-ttu-id="02856-155">Bazı üçüncü taraf sağlayıcılar kullanımı yaklaşımı önceki bölümde açıklanan dahil olmak üzere [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), ve [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="02856-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="02856-156">Her birinde ASP.NET oturum çekirdek içine takın veya ayrı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02856-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="02856-157">Serilog Günlükçü gönderilen tüm iletiler aşağıdakilere zenginleştirir bir özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="02856-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="02856-158">Bu özellik, hizmet adını, türünü ve bölüm bilgileri çıkarmak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="02856-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="02856-159">ASP.NET Core altyapısında bu özelliği kullanmak için bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="02856-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="02856-160">Serilog, Serilog.Extensions.Logging ve Serilog.Sinks.Observable NuGet paketlerini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="02856-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="02856-161">Sonraki örneğin Serilog.Sinks.Literate de ekleyin.</span><span class="sxs-lookup"><span data-stu-id="02856-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="02856-162">Daha iyi bir yaklaşım, bu makalenin sonraki bölümlerinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="02856-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="02856-163">Serilog içinde bir LoggerConfiguration ve Günlükçü örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="02856-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="02856-164">Hizmet oluşturucuya Serilog.ILogger bağımsız değişkeni eklemek ve yeni oluşturulan Günlükçü geçirin.</span><span class="sxs-lookup"><span data-stu-id="02856-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="02856-165">Hizmet oluşturucuda için özellik enrichers oluşturur aşağıdaki kodu ekleyin **ServiceTypeName**, **ServiceName**, **PartitionID**, ve **InstanceId** hizmetinin özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="02856-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="02856-166">Kodunuzda Microsoft.Extensions.Logging.ILogger kullanabilmeniz için ASP.NET Core günlük Fabrika için de bir özellik enricher ekler.</span><span class="sxs-lookup"><span data-stu-id="02856-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="02856-167">ASP.NET Core Serilog olmadan kullanıyormuş gibi kodu aynı izleme.</span><span class="sxs-lookup"><span data-stu-id="02856-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="02856-168">Önceki örnekle statik Log.Logger kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="02856-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="02856-169">Service Fabric aynı hizmet türünü tek bir işlem içinde birden çok örneğini barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="02856-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="02856-170">Statik Log.Logger kullanırsanız, özellik enrichers son yazan çalışan tüm örnekleri için değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="02856-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="02856-171">Bu neden _logger değişkeni bir hizmet sınıfında özel üye değişkeni nedenlerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="02856-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="02856-172">Ayrıca, _logger hizmetleri kullanılan ortak kodun kullanımına yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="02856-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="02856-173">Oturum açma sağlayıcısı seçme</span><span class="sxs-lookup"><span data-stu-id="02856-173">Choosing a logging provider</span></span>

<span data-ttu-id="02856-174">Uygulamanızı yüksek performans üzerinde dayalıysa **EventSource** genellikle iyi bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="02856-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="02856-175">**EventSource** *genellikle* daha az kaynak kullanır ve ASP.NET Core günlüğü ya da herhangi bir kullanılabilir üçüncü taraf çözümleri daha iyi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="02856-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="02856-176">Bu hizmet performans kullanarak dayalı olup olmadığını ancak birçok Hizmetleri için bir sorun değildir **EventSource** daha iyi bir seçim olabilir.</span><span class="sxs-lookup"><span data-stu-id="02856-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="02856-177">Ancak, bu yararları almak için günlüğe kaydetme, yapılandırılmış **EventSource** mühendislik ekibi daha büyük bir yatırım gerektirir.</span><span class="sxs-lookup"><span data-stu-id="02856-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="02856-178">Mümkünse, birkaç günlüğe kaydetme seçeneklerini hızlı prototipi yapın ve ardından ihtiyaçlarınıza en uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="02856-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02856-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02856-179">Next steps</span></span>

<span data-ttu-id="02856-180">Uygulamalar ve hizmetler işaretlemesini, oturum açma sağlayıcısı seçtikten sonra herhangi bir çözümleme platform gönderilmeden önce toplanacak günlüklerini ve olayları gerekir.</span><span class="sxs-lookup"><span data-stu-id="02856-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="02856-181">Hakkında bilgi edinin [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) ve [WAD](service-fabric-diagnostics-event-aggregation-wad.md) önerilen seçeneklerden bazıları daha iyi anlamak için.</span><span class="sxs-lookup"><span data-stu-id="02856-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
