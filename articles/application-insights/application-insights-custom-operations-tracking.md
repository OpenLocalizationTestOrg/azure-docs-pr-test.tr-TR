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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Application Insights .NET SDK ile özel işlemler izleme

Azure uygulama Insights SDK'ları otomatik olarak gelen HTTP isteklerini ve toodependent çağrıları izleme Hizmetleri, HTTP istekleri ve SQL sorguları gibi. İzleme ve istekleri ve bağımlılıkları bağıntı bu uygulamayı birleştirmek tüm mikro hizmetler arasında hello tüm uygulama yanıt hızını ve güvenilirlik görünürlük sağlar. 

Genel olarak desteklenen uygulama düzenleri sınıfının yoktur. Bu tür desenlerini izlemenin düzgün yapılabilmesi el ile kod araçları gerektirir. Bu makalede işleme ve uzun süre çalışan arka plan görevleri çalıştıran özel sıra gibi el ile araçları gerektirebilir birkaç desenleri kapsar.

Bu belge, tootrack özel işlemleriyle Application Insights SDK'sı nasıl hello rehberlik sağlar. Bu belge için geçerlidir:

- .NET (Temel SDK olarak da bilinir) sürüm 2.4 + için Application Insights.
- Web uygulamaları (ASP.NET çalıştıran) sürüm 2.4 + için Application Insights.
- ASP.NET Core sürüm 2.1 + için Application Insights.

## <a name="overview"></a>Genel Bakış
Bir mantıksal parça sahip bir uygulama tarafından çalıştırılan bir çalışma bir işlemdir. Başlangıç saati, süresi, sonuç ve kullanıcı adı, özellikler ve sonuç gibi yürütme bağlamı bir adı vardır. İşlem A B işlemi tarafından başlatıldı, sonra işlemi B A. için üst öğe olarak ayarlanır Bir işlemi yalnızca bir üst olabilir, ancak birçok alt işlemleri olabilir. İşlemler ve telemetri bağıntı hakkında daha fazla bilgi için bkz: [Azure Application Insights telemetri bağıntı](application-insights-correlation.md).

Hello Application Insights .NET SDK'sı, hello işlemi hello soyut sınıf tarafından açıklanan [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) ve alt öğeleri [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) ve [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Gelen işlemlerini izleme 
Merhaba Application Insights web SDK IIS ardışık düzeninde çalışan ASP.NET uygulamaları ve tüm ASP.NET Core uygulamaları HTTP isteklerini otomatik olarak toplar. Diğer platformlar ve altyapıları için topluluk tarafından desteklenen çözümleri vardır. Merhaba uygulaması herhangi bir hello standart veya topluluk tarafından desteklenen çözümleri desteklenmiyorsa, ancak, siz onu el ile işaretleyebilir.

Özel İzleme gerektiren başka bir öğe hello kuyruktan alır hello çalışan bir örnektir. Bazı kuyruklarında hello tooadd bağımlılık olarak toothis sıra izlenen bir ileti arayın. Ancak, ileti işleme açıklayan hello üst düzey işlemi otomatik olarak toplanmaz.

Biz bu tür işlemlerini nasıl izlemek görelim.

Yüksek bir düzeyde, hello toocreate bir görevdir `RequestTelemetry` ve bilinen özelliklerini ayarlama. Merhaba işlemi tamamlandıktan sonra hello telemetri izler. Bu görev aşağıdaki örneğine hello gösterir.

### <a name="http-request-in-owin-self-hosted-app"></a>HTTP isteği Owın kendini barındıran uygulama
Bu örnekte, biz hello izleyin [bağıntı için HTTP Protokolü](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). Var. açıklanan tooreceive üstbilgileri beklemelisiniz.

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

Merhaba bağıntı için HTTP protokolü ayrıca hello bildirir `Correlation-Context` üstbilgi. Ancak, kolaylık sağlamak için burada atlanır.

## <a name="queue-instrumentation"></a>Sıra Araçları
HTTP iletişimi için toopass bağıntı ayrıntıları bir protokol oluşturduk. Bazı sıraları protokollerle selamlama iletisine birlikte ve yapamazsınız başkalarıyla ek meta veri geçirebilirsiniz.

### <a name="service-bus-queue"></a>Hizmet veri yolu kuyruğu
Hello Azure ile [Service Bus kuyruğuna](../service-bus-messaging/index.md), bir özellik paketi selamlama iletisine birlikte geçirebilirsiniz. Biz toopass hello bağıntı kimliği kullanın

Merhaba Service Bus kuyruğuna TCP tabanlı protokollerini kullanır. Application Insights işlemlerini otomatik olarak izlemez sıra işlemleri biz bunları el ile izlemek için. Merhaba dequeue itme stili API bir işlemdir ve oluşturamıyor tootrack ki bunu.

#### <a name="enqueue"></a>Sıraya alma

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

#### <a name="process"></a>İşlem
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

### <a name="azure-storage-queue"></a>Azure depolama kuyruğu
örnekte gösterildiği nasıl aşağıdaki hello tootrack hello [Azure depolama kuyruğu](../storage/queues/storage-dotnet-how-to-use-queues.md) işlemler ve hello üretici, hello tüketici ve Azure Storage arasında correlate telemetri. 

Merhaba depolama kuyruğu bir HTTP API vardır. Tüm çağrıları toohello sırası, HTTP isteklerini hello uygulama Öngörüler bağımlılık toplayıcısı tarafından izlenir.
Olduğundan emin olun `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` içinde `applicationInsights.config`. Yoksa, program aracılığıyla açıklanan ekleme [filtreleme ve hello Azure Application Insights SDK'sı ön işleme](app-insights-api-filtering-sampling.md).

Application Insights el ile yapılandırırsanız, oluşturma ve başlatma emin olun `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` benzer şekilde:
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

Toocorrelate hello Application Insights işlem kimliği hello depolama istek kimliğiyle isteyebilirsiniz İstemci ve sunucu istek kimliği nasıl tooset ve bir depolama get isteği hakkında daha fazla bilgi için bkz: [izleme, tanılama ve Azure Storage sorun giderme](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>Sıraya alma
Depolama kuyrukları hello HTTP API desteklediğinden, tüm işlemleri hello sıra ile Application Insights tarafından otomatik olarak izlenir. Çoğu durumda, bu araçları yeterli olacaktır. Ancak, toocorrelate üretici izlemeleri ile Merhaba tüketici tarafında izler, bazı bağıntı bağlam geçmelidir benzer şekilde toohow biz bunu hello bağıntı için HTTP protokolü yapın. 

Bu örnekte, biz hello isteğe bağlı izlemek `Enqueue` işlemi. Şunları yapabilirsiniz:

 - **Yeniden deneme sayısı (varsa) ilişkilendirmek**: hello olan bir ortak üst sahip oldukları tüm `Enqueue` işlemi. Aksi takdirde hello gelen istek alt olarak izlenen. Birden çok mantıksal istekleri toohello sırası varsa, yeniden deneme içinde hangi çağrısı sonuçlandı zor toofind olabilir.
 - **Depolama günlükleri (varsa ve gerektiğinde) ilişkilendirmek**: Application Insights telemetri ile bağıntılı.

Merhaba `Enqueue` hello alt üst işleminin (örneğin, bir gelen HTTP istek) bir işlemdir. Merhaba HTTP bağımlılık çağrıdır hello hello alt `Enqueue` işlemi ve hello en alt hello gelen isteğin:

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

Uygulamanızı tooreduce hello telemetri miktarı raporları veya tootrack hello istememeniz `Enqueue` başka nedenlerle kullanım hello işlemi `Activity` doğrudan API:

- (Oluşturup başlatın) yeni bir `Activity` yerine hello Application Insights işlemi başlatılıyor. Bunu *değil* üzerindeki herhangi bir özellik hello işlem adı dışında tooassign gerekir.
- Seri hale `yourActivity.Id` hello ileti yükü yerine içine `operation.Telemetry.Id`. Aynı zamanda `Activity.Current.Id`.


#### <a name="dequeue"></a>Dequeue
Benzer şekilde çok`Enqueue`, gerçek bir HTTP isteği toohello depolama kuyruğu Application Insights tarafından otomatik olarak izlenir. Ancak, hello `Enqueue` işlemi büyük olasılıkla olur gelen bir istek bağlamı gibi hello üst bağlamında. Uygulama Insights SDK'ları otomatik olarak bu tür bir işlemi (ve HTTP bölümü) hello üst isteğiyle ilişkilendirmek ve başka telemetriyle hello aynı bildirilen kapsamı.

Merhaba `Dequeue` işlemdir hassas. Merhaba Application Insights SDK'sı, HTTP isteklerini otomatik olarak izler. Ancak, selamlama iletisine ayrıştırılır kadar hello bağıntı bağlam bilmiyor. Bu olası toocorrelate hello HTTP isteği tooget selamlama iletisine hello telemetri hello kalanıyla değil.

Çoğu durumda, yararlı toocorrelate hello HTTP istek toohello sırası diğer izlemeleri de sahip olabilir. Merhaba aşağıdaki örnekte gösterilmiştir nasıl toodo onu:

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

#### <a name="process"></a>İşlem

Aşağıdaki örneğine hello biz gelen ileti izleme bir şekilde benzer şekilde toohow biz izleme gelen HTTP istek:

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

Benzer şekilde, diğer kuyruk işlemlerini izleme eklenmiş. Peek işlemi benzer şekilde dequeue işlem olarak işaretlenir. Kuyruk yönetim işlemlerini izleme gerekli değildir. Application Insights HTTP gibi işlemleri izler ve çoğu durumda yeterlidir.

İleti silinmesini izleme zaman hello işlemi (bağıntı) tanımlayıcıları ayarladığınızdan emin olun. Alternatif olarak, hello kullanabilirsiniz `Activity` API. Ardından Application Insights, sizin yerinize yaptığından tooset işlemi tanımlayıcıları hello telemetri öğeler üzerinde gerekmez:

- Yeni bir `Activity` hello kuyruğundan öğeyi kurduktan sonra.
- Kullanım `Activity.SetParentId(message.ParentId)` toocorrelate tüketici ve üretici günlükleri.
- Merhaba Başlat `Activity`.
- İzleme dequeue, işlem ve silme işlemleri kullanarak `Start/StopOperation` Yardımcıları. Bunu hello zaman uyumsuz aynı denetimi akışını (yürütme bağlamı). Bu şekilde, bunların düzgün şekilde bağıntılı.
- Stop hello `Activity`.
- Kullanım `Start/StopOperation`, veya arama `Track` telemetri el ile.

### <a name="batch-processing"></a>Toplu işleme
Bazı kuyruklar, bir istek ile birden fazla ileti dequeue. Bu tür iletileri işleme büyük olasılıkla bağımsızdır ve toohello farklı mantıksal işlemlerini ait. Bu durumda, olası toocorrelate hello olmadığı `Dequeue` işlemi tooparticular ileti işleme.

Her ileti kendi zaman uyumsuz denetim akışı işlenmesi. Daha fazla bilgi için bkz: Merhaba [giden bağımlılıkları izleme](#outgoing-dependencies-tracking) bölümü.

## <a name="long-running-background-tasks"></a>Uzun süre çalışan arka plan görevleri
Bazı uygulamalar kullanıcı isteklerinden kaynaklanabilir uzun süre çalışan işlemlerini başlatın. Merhaba izleme/araçları açısından bakıldığında, istek veya bağımlılık izleme farklı değil: 

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

Bu örnekte, kullandığımız `telemetryClient.StartOperation` toocreate `RequestTelemetry` ve dolgu hello bağıntı bağlamı. Merhaba işlemi zamanlanan gelen istekler tarafından oluşturulan bir üst işlemi sahip varsayalım. Sürece `BackgroundTask` başlamasını Merhaba aynı zaman uyumsuz denetim akışı olarak gelen bir istek, o üst işlemi ile ilişkilendirilir. `BackgroundTask`ve tüm iç içe geçmiş telemetri öğeler otomatik olarak bile hello isteği sona erdikten sonra neden hello isteği ile ilişkili.

Başlangıç görevi, herhangi bir işlem yok hello arka plan iş parçacığından başladığında (`Activity`) ile ilişkili `BackgroundTask` herhangi bir üst sahip değil. Ancak, bu işlemleri iç içe. Merhaba görevden bildirilen tüm telemetri bağıntılı toohello öğeleridir `RequestTelemetry` oluşturulan `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Giden bağımlılıkları izleme
Kendi bağımlılık türü veya Application Insights tarafından desteklenmeyen bir işlem izleyebilirsiniz.

Merhaba `Enqueue` yöntemi hello hizmet veri yolu kuyruğu ya da hello depolama kuyruğu gibi özel izleme için örnek olarak hizmet verebilir.

için özel bağımlılık izleme için Hello genel yaklaşım şöyledir:

- Merhaba çağrısı `TelemetryClient.StartOperation` hello doldurur (uzantısı) yöntemi `DependencyTelemetry` bağıntı ve bazı diğer özellikler için gerekli olan özellikleri (başlangıç saati Damga, süre).
- Diğer özel özellikleri hello üzerinde ayarlamak `DependencyTelemetry`hello adı ve gereksinim duyduğunuz diğer bağlamı gibi.
- Arama ve bekleyin bir bağımlılık olun.
- Merhaba işlemi durdurmak `StopOperation` bu tamamlandığında.
- Özel durumları işleme.

`StopOperation`yalnızca başlatıldığından hello işlemini durdurur. Merhaba geçerli çalışan işlemin toostop, istediğiniz hello bir eşleşmiyorsa `StopOperation` hiçbir şey yapmaz. Hello paralel olarak birden çok işlemi başlatırsanız bu durum gerçekleşebilir aynı yürütme bağlamı:

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

Her zaman çağrı emin `StartOperation` ve göreviniz kendi bağlamında çalıştırın:
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

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba temel bilgileri öğrenmek [telemetri bağıntı](application-insights-correlation.md) Application ınsights'ta.
- Merhaba bkz [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- Özel rapor [olayları ve ölçümleri](app-insights-api-custom-events-metrics.md) tooApplication Insights.
- Standart denetleyin [yapılandırma](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) bağlam özellikleri koleksiyonu için.
- Merhaba denetleyin [System.Diagnostics.Activity Kullanıcı Kılavuzu](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee nasıl biz telemetrinin bağıntısını.
