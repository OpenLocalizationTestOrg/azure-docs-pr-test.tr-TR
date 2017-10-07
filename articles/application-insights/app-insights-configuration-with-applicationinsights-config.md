---
title: "aaaApplicationInsights.config başvuru - Azure | Microsoft Docs"
description: "Etkinleştirmek veya veri toplama modülleri devre dışı bırakın ve performans sayaçları ve diğer parametreleri ekleyin."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Merhaba Application Insights SDK'sı Applicationınsights.config veya .xml yapılandırma
Merhaba Application Insights .NET SDK'sı bir NuGet paketlerini oluşur. [Çekirdek paket](http://www.nuget.org/packages/Microsoft.ApplicationInsights) hello API hello Application Insights telemetri göndermesini sağlar. [Ek paket](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) telemetri sağlamak *modülleri* ve *başlatıcıları* telemetri uygulamanız ve onun içeriği otomatik olarak izlemek için. Hello yapılandırma dosyası ayarlayarak, etkinleştirmek veya telemetri modülleri ve başlatıcılar devre dışı bırakın ve bunların bazıları için parametreleri ayarlayın.

Merhaba yapılandırma dosyası adlı `ApplicationInsights.config` veya `ApplicationInsights.xml`bağlı olarak, uygulamanızın hello türü. Tooyour otomatik olarak eklenen ne zaman proje, [hello SDK çoğu sürümlerini yüklemek][start]. Tooa web uygulaması tarafından eklenir [Durum İzleyicisi bir IIS sunucusundaki][redfield], veya hello Appplication Öngörüler seçtiğinizde [bir Azure Web sitesine veya VM uzantısı](app-insights-azure-web-apps.md).

Bir eşdeğer dosya toocontrol hello hiç [SDK, bir web sayfasındaki][client].

Bu belgede, dosya, bunlar hello SDK ' hello bileşenlerinin nasıl kontrol ve bu bileşenleri hangi NuGet paketlerini yükleme hello yapılandırmasında bkz hello bölümleri açıklanmaktadır.

## <a name="telemetry-modules-aspnet"></a>Telemetri modülleri (ASP.NET)
Her bir telemetri modülü, belirli bir veri türü toplar ve hello çekirdek API toosend hello veri kullanır. Merhaba modülleri, ayrıca hello gerekli satırları toohello .config dosyası ekleyin farklı NuGet paketlerini tarafından yüklenir.

Merhaba yapılandırma dosyasındaki her modül için bir düğüm yok. toodisable bir modül hello düğümü silin veya açıklama çıkarın.

### <a name="dependency-tracking"></a>Bağımlılık izleme
[Bağımlılık izleme](app-insights-asp-net-dependencies.md) uygulamanızı yapar toodatabases ve dış hizmetler ve veritabanları çağrıları hakkında telemetri toplar. tooallow bu modülü toowork IIS Server çok ihtiyacınız[Durum İzleyicisi yükleme][redfield]. toouse bunu Azure web uygulamaları ya da sanal makineleri, [seçin hello Application Insights uzantısını](app-insights-azure-web-apps.md).

İzleme kodu hello kullanarak kendi bağımlılık de yazabilirsiniz [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet paketi.

### <a name="performance-collector"></a>Performans Toplayıcı
[Sistem performans sayaçlarını toplar](app-insights-performance-counters.md) gibi CPU, bellek ve ağ IIS yüklemelerinden yükleyin. Performans sayaçları, kendiniz ayarladığınız dahil olmak üzere hangi sayaçları toocollect belirtebilirsiniz.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet paketi.

### <a name="application-insights-diagnostics-telemetry"></a>Application Insights tanılama Telemetrisi
Merhaba `DiagnosticsTelemetryModule` hello Application Insights araçları kod kendisini hataları bildirir. Örneğin, performans sayaçları hello kod erişemiyorsanız veya bir `ITelemetryInitializer` bir özel durum oluşturur. Bu modülü tarafından izlenen izleme telemetri görünür hello [tanılama arama][diagnostic]. Tanılama veri toodc.services.vsallin.net gönderir.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet paketi. Yalnızca bu paketi yüklerseniz, hello Applicationınsights.config dosyası otomatik olarak oluşturulmaz.

### <a name="developer-mode"></a>Geliştirici modu
`DeveloperModeWithDebuggerAttachedTelemetryModule`zorlar hello Application Insights `TelemetryChannel` hemen toosend veri bir telemetri öğesi, her seferinde bir hata ayıklayıcısı olduğunda bağlı toohello uygulama işlemi. Bu, uygulamanızın telemetri izler ve hello Application Insights portalında görüntülendiğinde hello şu anda arasındaki süre hello miktarını azaltır. Önemli yükünü CPU ve ağ bant genişliği neden olur.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet paketi

### <a name="web-request-tracking"></a>Web isteği izleme
Raporları hello [yanıt süresi ve sonuç kodu](app-insights-asp-net.md) HTTP isteklerinin sayısıdır.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.applicationınsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet paketi

### <a name="exception-tracking"></a>Özel durum izleme
`ExceptionTrackingTelemetryModule`parçaları işlenmeyen özel durumlar web uygulamanızda. Bkz: [hataları ve özel durumları][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.applicationınsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet paketi
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-parçaları [görev özel durumlarını unobserved](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-çalışan rolleri, windows Hizmetleri ve konsol uygulamaları için işlenmeyen özel durumları izler.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet paketi.

### <a name="eventsource-tracking"></a>EventSource izleme
`EventSourceTelemetryModule`tooconfigure tooApplication Öngörüler izlemeleri gönderilen EventSource olaylarını toobe sağlar. EventSource olaylarını izleme hakkında daha fazla bilgi için bkz: [kullanarak EventSource olaylarını](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>ETW olay izleme
`EtwCollectorTelemetryModule`ETW sağlayıcılar toobe tooApplication Öngörüler izlemeleri gönderilen tooconfigure olayları sağlar. ETW olayları izleme hakkında daha fazla bilgi için bkz: [kullanarak ETW olayları](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
Merhaba Microsoft.ApplicationInsights paket sağlar hello [API çekirdek](https://msdn.microsoft.com/library/mt420197.aspx) hello SDK. Merhaba diğer telemetri modüller bunu kullanın ve ayrıca [toodefine kullanmak kendi telemetrinizi](app-insights-api-custom-events-metrics.md).

* Applicationınsights.config giriş yok.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet paketi. Yalnızca bu NuGet yüklerseniz, hiçbir .config dosyası oluşturulur.

## <a name="telemetry-channel"></a>Telemetri kanal
Merhaba telemetri kanal arabelleğe alma ve telemetri toohello Application Insights hizmeti aktarımını yönetir.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`Hizmetler için Hello varsayılan kanalıdır. Bu veri arabelleğe alır.
* `Microsoft.ApplicationInsights.PersistenceChannel`konsol uygulamaları için bir alternatiftir. Uygulamanızı kapatır ve hello uygulama yeniden başlatıldığında Gönder herhangi unflushed veri toopersistent depolama kaydedebilirsiniz.

## <a name="telemetry-initializers-aspnet"></a>Telemetri başlatıcıları (ASP.NET)
Telemetri başlatıcıları telemetrinin her öğesiyle birlikte gönderilir bağlam özellikleri ayarlayın.

Yapabilecekleriniz [kendi başlatıcıları yazma](app-insights-api-filtering-sampling.md#add-properties) tooset bağlam özellikleri.

Merhaba standart başlatıcıları tüm hello Web veya Windows Server NuGet paketleri tarafından ayarlanır:

* `AccountIdTelemetryInitializer`Merhaba AccountID özelliğini ayarlar.
* `AuthenticatedUserIdTelemetryInitializer`Merhaba AuthenticatedUserId özelliği hello JavaScript SDK'sı tarafından kümesi olarak ayarlar.
* `AzureRoleEnvironmentTelemetryInitializer`güncelleştirmeleri hello `RoleName` ve `RoleInstance` hello özelliklerini `Device` hello Azure çalışma zamanı ortamından ayıklanan bilgilerle tüm telemetri öğeleri için bağlamı.
* `BuildInfoConfigComponentVersionTelemetryInitializer`güncelleştirmeleri hello `Version` hello özelliğinin `Component` hello ayıklanan hello değere sahip tüm telemetri öğeleri bağlamının `BuildInfo.config` dosya MS Build tarafından üretilen.
* `ClientIpHeaderTelemetryInitializer`güncelleştirmeleri `Ip` hello özelliğinin `Location` tüm telemetri öğeleri bağlamında dayalı hello üzerinde `X-Forwarded-For` hello isteğin HTTP üstbilgisi.
* `DeviceTelemetryInitializer`Merhaba özelliklerini aşağıdaki güncelleştirmeleri hello `Device` tüm telemetri öğeleri için bağlamı.
  * `Type`çok Ayarla "PC"
  * `Id`Merhaba bilgisayarın etki alanı adını toohello Merhaba web uygulaması çalıştığı ayarlanır.
  * `OemName`Hello ayıklanan toohello değerini ayarlayın `Win32_ComputerSystem.Manufacturer` WMI kullanarak alan.
  * `Model`Hello ayıklanan toohello değerini ayarlayın `Win32_ComputerSystem.Model` WMI kullanarak alan.
  * `NetworkType`Hello ayıklanan toohello değerini ayarlayın `NetworkInterface`.
  * `Language`Merhaba toohello adına ayarlanır `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`güncelleştirmeleri hello `RoleInstance` hello özelliğinin `Device` hello etki alanı adına sahip tüm telemetri öğelerin hello bilgisayar Merhaba web uygulaması çalıştığı bağlam.
* `OperationNameTelemetryInitializer`güncelleştirmeleri hello `Name` hello özelliğinin `RequestTelemetry` ve hello `Name` hello özelliğinin `Operation` tüm telemetri öğeleri bağlamında dayalı hello HTTP yöntemi, yanı sıra üzerinde ASP.NET MVC denetleyicisi ve eylem çağrılan tooprocess hello adları İstek.
* `OperationIdTelemetryInitializer`veya `OperationCorrelationTelemetryInitializer` güncelleştirmeleri hello `Operation.Id` içerik özelliği tüm telemetri öğelerin izlenen hello ile otomatik olarak oluşturulan bir isteği işlerken `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`güncelleştirmeleri hello `Id` hello özelliğinin `Session` tüm telemetri öğeleri hello ayıklanan değerle bağlamının `ai_session` tanımlama bilgisi hello kullanıcının tarayıcısında çalışan Applicationınsights JavaScript araçları kodu hello tarafından oluşturulan.
* `SyntheticTelemetryInitializer`veya `SyntheticUserAgentTelemetryInitializer` güncelleştirmeleri hello `User`, `Session` ve `Operation` kullanılabilirlik test veya arama motoru bot gibi yapay bir kaynaktan bir isteği işlerken tüm telemetri öğelerinin bağlamları özellikleri izlenir. Varsayılan olarak, [ölçüm Gezgini](app-insights-metrics-explorer.md) yapay telemetri görüntülemez.

    Merhaba `<Filters>` hello isteklerinin özelliklerini tanımlayan ayarlayın.
* `UserAgentTelemetryInitializer`güncelleştirmeleri hello `UserAgent` hello özelliğinin `User` tüm telemetri öğeleri bağlamında dayalı hello üzerinde `User-Agent` hello isteğin HTTP üstbilgisi.
* `UserTelemetryInitializer`güncelleştirmeleri hello `Id` ve `AcquisitionDate` özelliklerini `User` hello ayıklanan değerlere sahip tüm telemetri öğeleri bağlamının `ai_user` hello çalışan hello uygulama Insights JavaScript araçları kodu tarafından oluşturulan tanımlama bilgisi Kullanıcının tarayıcısının.
* `WebTestTelemetryInitializer`ayarlar, kullanıcı kimliği, oturum kimliği ve yapay kaynak özelliklerini bu geliyor HTTP istekleri için hello [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md).
  Merhaba `<Filters>` hello isteklerinin özelliklerini tanımlayan ayarlayın.

Service Fabric çalışan .NET uygulamaları için hello içerebilir `Microsoft.ApplicationInsights.ServiceFabric` NuGet paketi. Bu paketi içeren bir `FabricTelemetryInitializer`, Service Fabric özellikleri tootelemetry öğeleri ekler. Daha fazla bilgi için bkz: Merhaba [GitHub sayfası](https://go.microsoft.com/fwlink/?linkid=848457) bu NuGet paketi tarafından eklenen hello özellikleri hakkında.

## <a name="telemetry-processors-aspnet"></a>Telemetri işlemci (ASP.NET)
Telemetri işlemciler filtre ve hello SDK toohello portalından gönderilmeden önce her bir telemetri öğeyi değiştirin.

Yapabilecekleriniz [kendi telemetri işlemciler yazma](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Uyarlamalı örnekleme telemetri işlemcisine (2.0.0-beta3)
Bu, varsayılan olarak etkindir. Uygulamanız çok sayıda telemetri gönderirse, bu işlemci bazıları da kaldırır.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

Merhaba parametresi tooachieve algoritması hello hello hedef çalışır sağlar. Sunucunuz birden fazla makine bir küme ise, telemetri gerçek hacmi hello uygun şekilde çarpılır şekilde hello her örneği SDK bağımsız olarak çalışır.

[Örnekleme hakkında daha fazla bilgi](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Sabit oran örnekleme telemetri işlemcisine (2.0.0-beta1)
Ayrıca bir standart olan [telemetri işlemci örnekleme](app-insights-api-filtering-sampling.md) (Başlangıç 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Kanal parametreleri (Java)
Bu parametreler hello Java SDK'sı nasıl ve depolamak topladığı hello telemetri verilerini temizleme etkiler.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
Merhaba hello SDK'ın bellek içi depolamada depolanan telemetri öğe sayısı. Bu sayıya ulaşıldığında, hello telemetri arabellek Temizlenen - hello telemetri öğeleri toohello Application Insights sunucusunun diğer bir deyişle, gönderilir.

* Min: 1
* En fazla: 1000
* Varsayılan: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Ne sıklıkta hello hello bellek içi depolamada depolanan verileri temizlendi (gönderilen tooApplication Öngörüler) olmayacağını belirler.

* Min: 1
* En fazla: 300
* Varsayılan: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Hello yerel diskteki toohello kalıcı depolama ayrılan MB cinsinden maksimum boyutu Hello belirler. Bu depolama aktarılan toobe toohello Application Insights endpoint başarısız kalıcı telemetri öğeleri için kullanılır. Merhaba depolama boyutu sağlandığında yeni telemetri öğeleri atılacak.

* Min: 1
* En fazla: 100
* Varsayılan: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Bu, verilerinizi göründüğü hello Application Insights kaynağı belirler. Genellikle, ayrı bir kaynak ayrı bir anahtarla her uygulamalarınız için oluşturun.

Uygulama toodifferent kaynaklarınızdan - toosend sonuçları istiyorsanız tooset hello anahtar dinamik olarak - örneğin istiyorsanız hello anahtar hello yapılandırma dosyasından atlayın ve bunun yerine kodda ayarlayın.

tooset hello anahtarını TelemetryClient, standart telemetri modüller de dahil olmak üzere tüm örnekleri için başlangıç anahtarı TelemetryConfiguration.Active ayarlayın. Bu, bir ASP.NET hizmetinde global.aspx.cs gibi başlatma yöntemini yapın:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Toosend yalnızca istiyorsanız olayları tooa farklı kaynak belirli bir ayarla, belirli bir TelemetryClient için başlangıç anahtarı ayarlayabilirsiniz:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

Yeni bir anahtar tooget [hello Application Insights portalında yeni bir kaynak oluşturmak][new].

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba API'si hakkında daha fazla bilgi][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
