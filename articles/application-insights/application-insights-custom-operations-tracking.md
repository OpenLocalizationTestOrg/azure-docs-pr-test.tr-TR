---
title: "Azure Application Insights .NET SDK'sı ile aaaTrack özel işlemler | Microsoft Docs"
description: "Azure Application Insights .NET SDK ile özel işlemler izleme"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="b4672-103">Application Insights .NET SDK ile özel işlemler izleme</span><span class="sxs-lookup"><span data-stu-id="b4672-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="b4672-104">Azure uygulama Insights SDK'ları otomatik olarak gelen HTTP isteklerini ve toodependent çağrıları izleme Hizmetleri, HTTP istekleri ve SQL sorguları gibi.</span><span class="sxs-lookup"><span data-stu-id="b4672-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="b4672-105">İzleme ve istekleri ve bağımlılıkları bağıntı bu uygulamayı birleştirmek tüm mikro hizmetler arasında hello tüm uygulama yanıt hızını ve güvenilirlik görünürlük sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4672-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="b4672-106">Genel olarak desteklenen uygulama düzenleri sınıfının yoktur.</span><span class="sxs-lookup"><span data-stu-id="b4672-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="b4672-107">Bu tür desenlerini izlemenin düzgün yapılabilmesi el ile kod araçları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b4672-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="b4672-108">Bu makalede işleme ve uzun süre çalışan arka plan görevleri çalıştıran özel sıra gibi el ile araçları gerektirebilir birkaç desenleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="b4672-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="b4672-109">Bu belge, tootrack özel işlemleriyle Application Insights SDK'sı nasıl hello rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4672-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="b4672-110">Bu belge için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="b4672-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="b4672-111">.NET (Temel SDK olarak da bilinir) sürüm 2.4 + için Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4672-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="b4672-112">Web uygulamaları (ASP.NET çalıştıran) sürüm 2.4 + için Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4672-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="b4672-113">ASP.NET Core sürüm 2.1 + için Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4672-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="b4672-114">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b4672-114">Overview</span></span>
<span data-ttu-id="b4672-115">Bir mantıksal parça sahip bir uygulama tarafından çalıştırılan bir çalışma bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b4672-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="b4672-116">Başlangıç saati, süresi, sonuç ve kullanıcı adı, özellikler ve sonuç gibi yürütme bağlamı bir adı vardır.</span><span class="sxs-lookup"><span data-stu-id="b4672-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="b4672-117">İşlem A B işlemi tarafından başlatıldı, sonra işlemi B A. için üst öğe olarak ayarlanır Bir işlemi yalnızca bir üst olabilir, ancak birçok alt işlemleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4672-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="b4672-118">İşlemler ve telemetri bağıntı hakkında daha fazla bilgi için bkz: [Azure Application Insights telemetri bağıntı](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="b4672-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="b4672-119">Hello Application Insights .NET SDK'sı, hello işlemi hello soyut sınıf tarafından açıklanan [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) ve alt öğeleri [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) ve [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="b4672-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="b4672-120">Gelen işlemlerini izleme</span><span class="sxs-lookup"><span data-stu-id="b4672-120">Incoming operations tracking</span></span> 
<span data-ttu-id="b4672-121">Merhaba Application Insights web SDK IIS ardışık düzeninde çalışan ASP.NET uygulamaları ve tüm ASP.NET Core uygulamaları HTTP isteklerini otomatik olarak toplar.</span><span class="sxs-lookup"><span data-stu-id="b4672-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="b4672-122">Diğer platformlar ve altyapıları için topluluk tarafından desteklenen çözümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="b4672-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="b4672-123">Merhaba uygulaması herhangi bir hello standart veya topluluk tarafından desteklenen çözümleri desteklenmiyorsa, ancak, siz onu el ile işaretleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b4672-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="b4672-124">Özel İzleme gerektiren başka bir öğe hello kuyruktan alır hello çalışan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="b4672-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="b4672-125">Bazı kuyruklarında hello tooadd bağımlılık olarak toothis sıra izlenen bir ileti arayın.</span><span class="sxs-lookup"><span data-stu-id="b4672-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="b4672-126">Ancak, ileti işleme açıklayan hello üst düzey işlemi otomatik olarak toplanmaz.</span><span class="sxs-lookup"><span data-stu-id="b4672-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="b4672-127">Biz bu tür işlemlerini nasıl izlemek görelim.</span><span class="sxs-lookup"><span data-stu-id="b4672-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="b4672-128">Yüksek bir düzeyde, hello toocreate bir görevdir `RequestTelemetry` ve bilinen özelliklerini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="b4672-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="b4672-129">Merhaba işlemi tamamlandıktan sonra hello telemetri izler.</span><span class="sxs-lookup"><span data-stu-id="b4672-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="b4672-130">Bu görev aşağıdaki örneğine hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4672-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="b4672-131">HTTP isteği Owın kendini barındıran uygulama</span><span class="sxs-lookup"><span data-stu-id="b4672-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="b4672-132">Bu örnekte, biz hello izleyin [bağıntı için HTTP Protokolü](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="b4672-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="b4672-133">Var. açıklanan tooreceive üstbilgileri beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b4672-133">You should expect tooreceive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="b4672-134">Merhaba bağıntı için HTTP protokolü ayrıca hello bildirir `Correlation-Context` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="b4672-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="b4672-135">Ancak, kolaylık sağlamak için burada atlanır.</span><span class="sxs-lookup"><span data-stu-id="b4672-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="b4672-136">Sıra Araçları</span><span class="sxs-lookup"><span data-stu-id="b4672-136">Queue instrumentation</span></span>
<span data-ttu-id="b4672-137">HTTP iletişimi için toopass bağıntı ayrıntıları bir protokol oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="b4672-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="b4672-138">Bazı sıraları protokollerle selamlama iletisine birlikte ve yapamazsınız başkalarıyla ek meta veri geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4672-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="b4672-139">Hizmet veri yolu kuyruğu</span><span class="sxs-lookup"><span data-stu-id="b4672-139">Service Bus queue</span></span>
<span data-ttu-id="b4672-140">Hello Azure ile [Service Bus kuyruğuna](../service-bus-messaging/index.md), bir özellik paketi selamlama iletisine birlikte geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4672-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="b4672-141">Biz toopass hello bağıntı kimliği kullanın</span><span class="sxs-lookup"><span data-stu-id="b4672-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="b4672-142">Merhaba Service Bus kuyruğuna TCP tabanlı protokollerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b4672-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="b4672-143">Application Insights işlemlerini otomatik olarak izlemez sıra işlemleri biz bunları el ile izlemek için.</span><span class="sxs-lookup"><span data-stu-id="b4672-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="b4672-144">Merhaba dequeue itme stili API bir işlemdir ve oluşturamıyor tootrack ki bunu.</span><span class="sxs-lookup"><span data-stu-id="b4672-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="b4672-145">Sıraya alma</span><span class="sxs-lookup"><span data-stu-id="b4672-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="b4672-146">İşlem</span><span class="sxs-lookup"><span data-stu-id="b4672-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="b4672-147">Azure depolama kuyruğu</span><span class="sxs-lookup"><span data-stu-id="b4672-147">Azure Storage queue</span></span>
<span data-ttu-id="b4672-148">örnekte gösterildiği nasıl aşağıdaki hello tootrack hello [Azure depolama kuyruğu](../storage/queues/storage-dotnet-how-to-use-queues.md) işlemler ve hello üretici, hello tüketici ve Azure Storage arasında correlate telemetri.</span><span class="sxs-lookup"><span data-stu-id="b4672-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="b4672-149">Merhaba depolama kuyruğu bir HTTP API vardır.</span><span class="sxs-lookup"><span data-stu-id="b4672-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="b4672-150">Tüm çağrıları toohello sırası, HTTP isteklerini hello uygulama Öngörüler bağımlılık toplayıcısı tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="b4672-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="b4672-151">Olduğundan emin olun `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` içinde `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="b4672-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="b4672-152">Yoksa, program aracılığıyla açıklanan ekleme [filtreleme ve hello Azure Application Insights SDK'sı ön işleme](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b4672-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="b4672-153">Application Insights el ile yapılandırırsanız, oluşturma ve başlatma emin olun `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` benzer şekilde:</span><span class="sxs-lookup"><span data-stu-id="b4672-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="b4672-154">Toocorrelate hello Application Insights işlem kimliği hello depolama istek kimliğiyle isteyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b4672-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="b4672-155">İstemci ve sunucu istek kimliği nasıl tooset ve bir depolama get isteği hakkında daha fazla bilgi için bkz: [izleme, tanılama ve Azure Storage sorun giderme](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="b4672-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="b4672-156">Sıraya alma</span><span class="sxs-lookup"><span data-stu-id="b4672-156">Enqueue</span></span>
<span data-ttu-id="b4672-157">Depolama kuyrukları hello HTTP API desteklediğinden, tüm işlemleri hello sıra ile Application Insights tarafından otomatik olarak izlenir.</span><span class="sxs-lookup"><span data-stu-id="b4672-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="b4672-158">Çoğu durumda, bu araçları yeterli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b4672-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="b4672-159">Ancak, toocorrelate üretici izlemeleri ile Merhaba tüketici tarafında izler, bazı bağıntı bağlam geçmelidir benzer şekilde toohow biz bunu hello bağıntı için HTTP protokolü yapın.</span><span class="sxs-lookup"><span data-stu-id="b4672-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="b4672-160">Bu örnekte, biz hello isteğe bağlı izlemek `Enqueue` işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4672-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="b4672-161">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4672-161">You can:</span></span>

 - <span data-ttu-id="b4672-162">**Yeniden deneme sayısı (varsa) ilişkilendirmek**: hello olan bir ortak üst sahip oldukları tüm `Enqueue` işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4672-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="b4672-163">Aksi takdirde hello gelen istek alt olarak izlenen.</span><span class="sxs-lookup"><span data-stu-id="b4672-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="b4672-164">Birden çok mantıksal istekleri toohello sırası varsa, yeniden deneme içinde hangi çağrısı sonuçlandı zor toofind olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4672-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="b4672-165">**Depolama günlükleri (varsa ve gerektiğinde) ilişkilendirmek**: Application Insights telemetri ile bağıntılı.</span><span class="sxs-lookup"><span data-stu-id="b4672-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="b4672-166">Merhaba `Enqueue` hello alt üst işleminin (örneğin, bir gelen HTTP istek) bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b4672-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="b4672-167">Merhaba HTTP bağımlılık çağrıdır hello hello alt `Enqueue` işlemi ve hello en alt hello gelen isteğin:</span><span class="sxs-lookup"><span data-stu-id="b4672-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="b4672-168">Uygulamanızı tooreduce hello telemetri miktarı raporları veya tootrack hello istememeniz `Enqueue` başka nedenlerle kullanım hello işlemi `Activity` doğrudan API:</span><span class="sxs-lookup"><span data-stu-id="b4672-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="b4672-169">(Oluşturup başlatın) yeni bir `Activity` yerine hello Application Insights işlemi başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="b4672-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="b4672-170">Bunu *değil* üzerindeki herhangi bir özellik hello işlem adı dışında tooassign gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4672-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="b4672-171">Seri hale `yourActivity.Id` hello ileti yükü yerine içine `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="b4672-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="b4672-172">Aynı zamanda `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="b4672-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="b4672-173">Dequeue</span><span class="sxs-lookup"><span data-stu-id="b4672-173">Dequeue</span></span>
<span data-ttu-id="b4672-174">Benzer şekilde çok`Enqueue`, gerçek bir HTTP isteği toohello depolama kuyruğu Application Insights tarafından otomatik olarak izlenir.</span><span class="sxs-lookup"><span data-stu-id="b4672-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="b4672-175">Ancak, hello `Enqueue` işlemi büyük olasılıkla olur gelen bir istek bağlamı gibi hello üst bağlamında.</span><span class="sxs-lookup"><span data-stu-id="b4672-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="b4672-176">Uygulama Insights SDK'ları otomatik olarak bu tür bir işlemi (ve HTTP bölümü) hello üst isteğiyle ilişkilendirmek ve başka telemetriyle hello aynı bildirilen kapsamı.</span><span class="sxs-lookup"><span data-stu-id="b4672-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="b4672-177">Merhaba `Dequeue` işlemdir hassas.</span><span class="sxs-lookup"><span data-stu-id="b4672-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="b4672-178">Merhaba Application Insights SDK'sı, HTTP isteklerini otomatik olarak izler.</span><span class="sxs-lookup"><span data-stu-id="b4672-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="b4672-179">Ancak, selamlama iletisine ayrıştırılır kadar hello bağıntı bağlam bilmiyor.</span><span class="sxs-lookup"><span data-stu-id="b4672-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="b4672-180">Bu olası toocorrelate hello HTTP isteği tooget selamlama iletisine hello telemetri hello kalanıyla değil.</span><span class="sxs-lookup"><span data-stu-id="b4672-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="b4672-181">Çoğu durumda, yararlı toocorrelate hello HTTP istek toohello sırası diğer izlemeleri de sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4672-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="b4672-182">Merhaba aşağıdaki örnekte gösterilmiştir nasıl toodo onu:</span><span class="sxs-lookup"><span data-stu-id="b4672-182">hello following example demonstrates how toodo it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="b4672-183">İşlem</span><span class="sxs-lookup"><span data-stu-id="b4672-183">Process</span></span>

<span data-ttu-id="b4672-184">Aşağıdaki örneğine hello biz gelen ileti izleme bir şekilde benzer şekilde toohow biz izleme gelen HTTP istek:</span><span class="sxs-lookup"><span data-stu-id="b4672-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="b4672-185">Benzer şekilde, diğer kuyruk işlemlerini izleme eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="b4672-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="b4672-186">Peek işlemi benzer şekilde dequeue işlem olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="b4672-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="b4672-187">Kuyruk yönetim işlemlerini izleme gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b4672-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="b4672-188">Application Insights HTTP gibi işlemleri izler ve çoğu durumda yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="b4672-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="b4672-189">İleti silinmesini izleme zaman hello işlemi (bağıntı) tanımlayıcıları ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b4672-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="b4672-190">Alternatif olarak, hello kullanabilirsiniz `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="b4672-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="b4672-191">Ardından Application Insights, sizin yerinize yaptığından tooset işlemi tanımlayıcıları hello telemetri öğeler üzerinde gerekmez:</span><span class="sxs-lookup"><span data-stu-id="b4672-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="b4672-192">Yeni bir `Activity` hello kuyruğundan öğeyi kurduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="b4672-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="b4672-193">Kullanım `Activity.SetParentId(message.ParentId)` toocorrelate tüketici ve üretici günlükleri.</span><span class="sxs-lookup"><span data-stu-id="b4672-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="b4672-194">Merhaba Başlat `Activity`.</span><span class="sxs-lookup"><span data-stu-id="b4672-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="b4672-195">İzleme dequeue, işlem ve silme işlemleri kullanarak `Start/StopOperation` Yardımcıları.</span><span class="sxs-lookup"><span data-stu-id="b4672-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="b4672-196">Bunu hello zaman uyumsuz aynı denetimi akışını (yürütme bağlamı).</span><span class="sxs-lookup"><span data-stu-id="b4672-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="b4672-197">Bu şekilde, bunların düzgün şekilde bağıntılı.</span><span class="sxs-lookup"><span data-stu-id="b4672-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="b4672-198">Stop hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="b4672-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="b4672-199">Kullanım `Start/StopOperation`, veya arama `Track` telemetri el ile.</span><span class="sxs-lookup"><span data-stu-id="b4672-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="b4672-200">Toplu işleme</span><span class="sxs-lookup"><span data-stu-id="b4672-200">Batch processing</span></span>
<span data-ttu-id="b4672-201">Bazı kuyruklar, bir istek ile birden fazla ileti dequeue.</span><span class="sxs-lookup"><span data-stu-id="b4672-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="b4672-202">Bu tür iletileri işleme büyük olasılıkla bağımsızdır ve toohello farklı mantıksal işlemlerini ait.</span><span class="sxs-lookup"><span data-stu-id="b4672-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="b4672-203">Bu durumda, olası toocorrelate hello olmadığı `Dequeue` işlemi tooparticular ileti işleme.</span><span class="sxs-lookup"><span data-stu-id="b4672-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="b4672-204">Her ileti kendi zaman uyumsuz denetim akışı işlenmesi.</span><span class="sxs-lookup"><span data-stu-id="b4672-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="b4672-205">Daha fazla bilgi için bkz: Merhaba [giden bağımlılıkları izleme](#outgoing-dependencies-tracking) bölümü.</span><span class="sxs-lookup"><span data-stu-id="b4672-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="b4672-206">Uzun süre çalışan arka plan görevleri</span><span class="sxs-lookup"><span data-stu-id="b4672-206">Long-running background tasks</span></span>
<span data-ttu-id="b4672-207">Bazı uygulamalar kullanıcı isteklerinden kaynaklanabilir uzun süre çalışan işlemlerini başlatın.</span><span class="sxs-lookup"><span data-stu-id="b4672-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="b4672-208">Merhaba izleme/araçları açısından bakıldığında, istek veya bağımlılık izleme farklı değil:</span><span class="sxs-lookup"><span data-stu-id="b4672-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="b4672-209">Bu örnekte, kullandığımız `telemetryClient.StartOperation` toocreate `RequestTelemetry` ve dolgu hello bağıntı bağlamı.</span><span class="sxs-lookup"><span data-stu-id="b4672-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="b4672-210">Merhaba işlemi zamanlanan gelen istekler tarafından oluşturulan bir üst işlemi sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b4672-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="b4672-211">Sürece `BackgroundTask` başlamasını Merhaba aynı zaman uyumsuz denetim akışı olarak gelen bir istek, o üst işlemi ile ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="b4672-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="b4672-212">`BackgroundTask`ve tüm iç içe geçmiş telemetri öğeler otomatik olarak bile hello isteği sona erdikten sonra neden hello isteği ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="b4672-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="b4672-213">Başlangıç görevi, herhangi bir işlem yok hello arka plan iş parçacığından başladığında (`Activity`) ile ilişkili `BackgroundTask` herhangi bir üst sahip değil.</span><span class="sxs-lookup"><span data-stu-id="b4672-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="b4672-214">Ancak, bu işlemleri iç içe.</span><span class="sxs-lookup"><span data-stu-id="b4672-214">However, it can have nested operations.</span></span> <span data-ttu-id="b4672-215">Merhaba görevden bildirilen tüm telemetri bağıntılı toohello öğeleridir `RequestTelemetry` oluşturulan `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="b4672-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="b4672-216">Giden bağımlılıkları izleme</span><span class="sxs-lookup"><span data-stu-id="b4672-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="b4672-217">Kendi bağımlılık türü veya Application Insights tarafından desteklenmeyen bir işlem izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4672-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="b4672-218">Merhaba `Enqueue` yöntemi hello hizmet veri yolu kuyruğu ya da hello depolama kuyruğu gibi özel izleme için örnek olarak hizmet verebilir.</span><span class="sxs-lookup"><span data-stu-id="b4672-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="b4672-219">için özel bağımlılık izleme için Hello genel yaklaşım şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b4672-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="b4672-220">Merhaba çağrısı `TelemetryClient.StartOperation` hello doldurur (uzantısı) yöntemi `DependencyTelemetry` bağıntı ve bazı diğer özellikler için gerekli olan özellikleri (başlangıç saati Damga, süre).</span><span class="sxs-lookup"><span data-stu-id="b4672-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="b4672-221">Diğer özel özellikleri hello üzerinde ayarlamak `DependencyTelemetry`hello adı ve gereksinim duyduğunuz diğer bağlamı gibi.</span><span class="sxs-lookup"><span data-stu-id="b4672-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="b4672-222">Arama ve bekleyin bir bağımlılık olun.</span><span class="sxs-lookup"><span data-stu-id="b4672-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="b4672-223">Merhaba işlemi durdurmak `StopOperation` bu tamamlandığında.</span><span class="sxs-lookup"><span data-stu-id="b4672-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="b4672-224">Özel durumları işleme.</span><span class="sxs-lookup"><span data-stu-id="b4672-224">Handle exceptions.</span></span>

<span data-ttu-id="b4672-225">`StopOperation`yalnızca başlatıldığından hello işlemini durdurur.</span><span class="sxs-lookup"><span data-stu-id="b4672-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="b4672-226">Merhaba geçerli çalışan işlemin toostop, istediğiniz hello bir eşleşmiyorsa `StopOperation` hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="b4672-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="b4672-227">Hello paralel olarak birden çok işlemi başlatırsanız bu durum gerçekleşebilir aynı yürütme bağlamı:</span><span class="sxs-lookup"><span data-stu-id="b4672-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="b4672-228">Her zaman çağrı emin `StartOperation` ve göreviniz kendi bağlamında çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b4672-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b4672-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4672-229">Next steps</span></span>

- <span data-ttu-id="b4672-230">Merhaba temel bilgileri öğrenmek [telemetri bağıntı](application-insights-correlation.md) Application ınsights'ta.</span><span class="sxs-lookup"><span data-stu-id="b4672-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="b4672-231">Merhaba bkz [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="b4672-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="b4672-232">Özel rapor [olayları ve ölçümleri](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="b4672-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="b4672-233">Standart denetleyin [yapılandırma](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) bağlam özellikleri koleksiyonu için.</span><span class="sxs-lookup"><span data-stu-id="b4672-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="b4672-234">Merhaba denetleyin [System.Diagnostics.Activity Kullanıcı Kılavuzu](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee nasıl biz telemetrinin bağıntısını.</span><span class="sxs-lookup"><span data-stu-id="b4672-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
