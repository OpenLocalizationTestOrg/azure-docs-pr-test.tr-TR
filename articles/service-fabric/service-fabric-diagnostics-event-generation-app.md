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
# <a name="application-and-service-level-event-and-log-generation"></a>Uygulama ve hizmet düzeyi olay ve günlük oluşturma

## <a name="instrumenting-hello-code-with-custom-events"></a>Özel olaylar Hello koduyla düzenleme

Merhaba kod düzenleme hello çoğu diğer yönlerini hizmetlerinizi izleme temelini oluşturur. İzleme, bir şeyler yanlış ve toodiagnose ne sabit toobe gerektiğini biliyor hello tek yoludur. Teknik olarak olası tooconnect bir hata ayıklayıcı tooa üretim hizmeti olmasına rağmen ortak bir uygulama değildir. Bu nedenle, izleme verileri ayrıntılı önemlidir.

Bazı ürünler kodunuzu otomatik olarak işaretleme. Bu çözüm de olsa da, el ile araçları neredeyse her zaman gereklidir. Merhaba bitimine hello uygulamanızın hatalarını ayıklama yeterli bilgi tooforensically olması gerekir. Bu belge, kodunuzu farklı yaklaşımlara tooinstrumenting açıklar ve ne zaman toochoose bir yaklaşımını başka bir.

## <a name="eventsource"></a>EventSource
Visual Studio'da bir şablondan bir Service Fabric çözüm oluşturduğunuzda bir **EventSource**-türetilen sınıfı (**ServiceEventSource** veya **ActorEventSource**) oluşturulur. Bir şablon oluşturduğunuzu, uygulama veya hizmet için olayları ekleyebilirsiniz. Merhaba **EventSource** adı **gerekir** benzersiz olmalı ve hello varsayılan şablon dizeden Şirketim - adlandırılmamalıdır&lt;çözüm&gt; - &lt; Proje&gt;. Birden çok sahip **EventSource** kullanan tanımları hello bir sorununu çalışma zamanında aynı adı neden olur. Her tanımlanan olay benzersiz bir tanımlayıcı olması gerekir. Tanımlayıcı benzersiz değilse, bir çalışma zamanı hatası oluşur. Bazı kuruluşlar ayrı geliştirme ekipleri arasında tanımlayıcıları tooavoid çakışmalar için değerleri aralığı preassign. Daha fazla bilgi için bkz: [Vance'nın blogu](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) veya hello [MSDN belgelerine](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>Yapılandırılmış EventSource olaylarını kullanma

Bu bölümdeki hello kod örneklerde hello olayların her biri tanımlanmış için belirli bir durumda, örneğin, bir hizmet türünün kaydedildiğinde. Kullanım örneği tarafından iletileri tanımlamak, veri hello hata hello metinle paketlenmesi ve şunları yapabilirsiniz daha kolayca arama ve filtre hello adları veya hello değerlerini temel alarak özellikleri belirtilmiş. Hello araç çıktısının yapılandırılması daha kolay tooconsume kolaylaştırır, ancak daha fazla düşünce gerektirir ve her kullanım örneği için yeni bir olay toodefine saat. Bazı olay tanımları hello tüm uygulama arasında paylaşılabilir. Örneğin, bir yöntemi Başlat veya Durdur için olay uygulama içinde birçok hizmetlerde yeniden. Bir sipariş sistemi gibi bir etki alanına özgü hizmet olabilir bir **CreateOrder** kendi benzersiz olayın olay. Bu yaklaşım birçok olayları oluşturmak ve potansiyel olarak tanımlayıcıları proje ekipleri arasında gerektiren. 

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

### <a name="using-eventsource-generically"></a>EventSource genel kullanma

Belirli olayları tanımlama zor olabilir çünkü çoğu kişi genellikle dize olarak kendi bilgilerini çıktı parametreleri ortak bir dizi birkaç olaylarla tanımlayın. Yapılandırılmış hello en boy çoğunu kaybolur ve daha zor toosearch ve filtre hello sonuçları değil. Bu yaklaşımda, genellikle toohello günlük düzeylerini karşılık birkaç olaylar tanımlanır. Aşağıdaki kod parçacığında hello hata ayıklama ve hata iletisini tanımlar:

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

Karma yapılandırılmış ve genel araçları kullanarak da iyi çalışabilir. Yapılandırılmış araçları hataları ve ölçümleri raporlama için kullanılır. Genel olaylar ayrıntılı hello için kullanılabilir diğer bir deyişle oturum tüketilen mühendisleri tarafından sorun giderme için.

## <a name="aspnet-core-logging"></a>ASP.NET oturum çekirdek

Buna ait önemli toocarefully planlama kodunuzu nasıl izleme. Merhaba sağ araçları planı büyük olasılıkla kodunuzu temel destabilizing ve tooreinstrument hello kod ihtiyaç duyan önlemenize yardımcı olabilir. tooreduce risk gibi bir araç kitaplığı seçebilirsiniz [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), Microsoft ASP.NET Core parçası olduğu. ASP.NET Core sahip bir [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) var olan kodu hello etkisini en aza indirerek tercih ettiğiniz hello sağlayıcı ile kullanabileceğiniz arabirimi. Windows ve Linux üzerinde ASP.NET Core hello kodu kullanın ve araçları kodunuzu standartlaştırılmış şekilde hello .NET Framework tam. Bu daha aşağıda incelediniz:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Service Fabric Microsoft.Extensions.Logging kullanma

1. Merhaba tooinstrument istediğiniz Microsoft.Extensions.Logging NuGet paketi toohello proje ekleyin. Ayrıca, herhangi bir sağlayıcı paket ekleme (üçüncü taraf paketi için aşağıdaki örneğine hello bakın). Daha fazla bilgi için bkz: [ASP.NET çekirdek günlüğü](https://docs.microsoft.com/aspnet/core/fundamentals/logging).
2. Ekleme bir **kullanarak** Microsoft.Extensions.Logging tooyour hizmet dosyası için yönerge.
3. Hizmet sınıfınızı içinde özel bir değişken tanımlayın.

  ```csharp
  private ILogger _logger = null;

  ```
4. Hizmet sınıfınızı Hello oluşturucuda bu kodu ekleyin:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Yöntemlerinizi kodunuzda izleme başlatın. Bazı örnekler şunlardır:

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Diğer günlük sağlayıcıları kullanma

Bazı üçüncü taraf sağlayıcılar hello önceki bölümünde açıklanan hello yaklaşımı kullanmak da dahil olmak üzere [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), ve [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). Her birinde ASP.NET oturum çekirdek içine takın veya ayrı olarak kullanabilirsiniz. Serilog Günlükçü gönderilen tüm iletiler aşağıdakilere zenginleştirir bir özelliği vardır. Bu özellik kullanışlı toooutput hello hizmet adını, türünü ve bölüm bilgileri olabilir. toouse bu özelliği hello ASP.NET Core altyapı de şu adımları yapın:

1. Serilog, Serilog.Extensions.Logging, hello ve toohello proje Serilog.Sinks.Observable NuGet paketleri ekleyin. Merhaba sonraki örnekte, ayrıca Serilog.Sinks.Literate ekleyin. Daha iyi bir yaklaşım, bu makalenin sonraki bölümlerinde gösterilir.
2. Serilog içinde LoggerConfiguration ve hello Günlükçü örneği oluşturun.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Bir Serilog.ILogger bağımsız değişkeni toohello hizmet oluşturucu ekleyin ve Günlükçü yeni oluşturulan hello geçirin.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. Merhaba hizmet oluşturucuda hello hello özelliği enrichers oluşturur kod aşağıdaki hello eklemek **ServiceTypeName**, **ServiceName**, **PartitionID**ve  **InstanceId** hello hizmetinin özelliklerini. Kodunuzda Microsoft.Extensions.Logging.ILogger kullanabilmeniz için ayrıca bir özelliği enricher toohello ASP.NET Core günlük Fabrika ekler.

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

5. Gereç hello kod hello aynı ASP.NET Core Serilog olmadan kullanıyormuş gibi.

  >[!NOTE]
  >Merhaba statik kullanmamanızı öneririz Log.Logger örnek önceki hello ile. Service Fabric birden çok ana bilgisayar aynı hizmeti Merhaba tek bir işlem içinde türü. Kullanırsanız, statik Log.Logger Merhaba, hello özelliği enrichers hello son yazan çalışan tüm örnekleri için değerleri gösterir. Bu neden hello _logger değişkeni hello hizmet sınıfı bir özel üye değişkeni nedenlerinden biridir. Ayrıca, hizmetleri kullanılan hello _logger kullanılabilir toocommon kod yapmanız gerekir.

## <a name="choosing-a-logging-provider"></a>Oturum açma sağlayıcısı seçme

Uygulamanızı yüksek performans üzerinde dayalıysa **EventSource** genellikle iyi bir yaklaşımdır. **EventSource** *genellikle* daha az kaynak kullanır ve ASP.NET Core günlüğü ya da herhangi bir hello kullanılabilir üçüncü taraf çözümleri daha iyi gerçekleştirir.  Bu hizmet performans kullanarak dayalı olup olmadığını ancak birçok Hizmetleri için bir sorun değildir **EventSource** daha iyi bir seçim olabilir. Ancak, günlük, tooget bu yararları yapılandırılmış **EventSource** mühendislik ekibi daha büyük bir yatırım gerektirir. Mümkünse, birkaç günlüğe kaydetme seçeneklerini hızlı prototipi yapın ve ardından hello gereksinimlerinizi en iyi karşılayan bir tane seçin.

## <a name="next-steps"></a>Sonraki adımlar

Uygulamalar ve hizmetler günlüğü sağlayıcısı tooinstrument seçtikten sonra günlüklerini ve olayları tooany analiz platformu gönderilmeden önce bir araya getirilir toobe gerekir. Hakkında bilgi edinin [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) ve [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter bazı seçenekleri önerilen hello anlama.
