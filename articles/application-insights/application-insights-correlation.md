---
title: "aaaAzure uygulama Insights Telemetri bağıntı | Microsoft Docs"
description: "Uygulama Insights telemetri bağıntı"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Application ınsights'ta telemetri bağıntı

Mikro hizmetlerin Hello world hello hizmet çeşitli bileşenlerinin işleri her mantıksal işlem gerektirir. Bu bileşenlerin her birini tarafından ayrı olarak izlenebilir [Application Insights](app-insights-overview.md). Merhaba web uygulaması bileşeni, kimlik doğrulama sağlayıcısı bileşen toovalidate kullanıcı kimlik bilgileriyle ve hello API bileşeni tooget veri görselleştirme ile iletişim kurar. Merhaba API bileşeni, dönüş diğer hizmetlerden verileri sorgulamak ve önbelleği sağlayıcısı bileşenlerini kullanabilir ve hello fatura bileşeni bu çağrıyı hakkında bildirim. Uygulama Öngörüler destekler dağıtılmış telemetri bağıntı. Hangi bileşenin hatalar veya performans düşüşü sorumlu toodetect sağlar.

Bu makalede, Application Insights toocorrelate telemetri tarafından kullanılan hello veri modelini birden çok bileşen tarafından gönderilen açıklanmaktadır. Merhaba bağlam yayma teknikleri ve protokolleri kapsar. Merhaba uygulama farklı diller ve platformlarda hello bağıntı kavramlarını ele alınmaktadır.

## <a name="telemetry-correlation-data-model"></a>Telemetri bağıntı veri modeli

Application Insights tanımlayan bir [veri modeli](application-insights-data-model.md) dağıtılmış telemetri bağıntı için. tooassociate telemetri hello mantıksal işlemi ile her telemetri öğenin sahip adlı bir bağlam alan `operation_Id`. Bu tanımlayıcı her telemetri öğesi tarafından dağıtılan hello izlemede paylaşılır. Bu nedenle bile telemetri tek bir katmandan kaybı ile hala diğer bileşenler tarafından bildirilen telemetri ilişkilendirebilirsiniz.

Dağıtılmış mantıksal işlemi genellikle daha küçük işlemleri - hello bileşenlerden biri tarafından işlenen isteklerin kümesi oluşur. Bu işlemler tarafından tanımlanan [isteği telemetri](application-insights-data-model-request-telemetry.md). Her istek telemetri kendi sahip `id` , genel olarak benzersiz şekilde tanımlar. Ve tüm telemetri - izlemeleri, özel durumlar, bu istekle ilişkili vb. hello ayarlamalısınız `operation_parentId` hello isteği toohello değerini `id`.

Her giden işlem tarafından temsil edilen http çağrısı tooanother bileşeni gibi [bağımlılık telemetrisi](application-insights-data-model-dependency-telemetry.md). Bağımlılık telemetrisi ayrıca tanımlar kendi `id` genel olarak benzersiz. Bu bağımlılık çağrısı tarafından başlatılan isteği telemetri olarak kullanan `operation_parentId`.

Dağıtılmış mantıksal işlemi kullanarak hello görünümünü oluşturabilirsiniz `operation_Id`, `operation_parentId`, ve `request.id` ile `dependency.id`. Bu alanlar aynı zamanda hello causality telemetri çağrıları sırasını tanımlar.

Mikro Hizmetleri ortamında bileşenleri izlemeleri toohello farklı depolarını gidebilir. Her bileşen, kendi izleme anahtarını Application Insights'ta olabilir. tooget telemetri hello mantıksal işlem için her depolama biriminden tooquery verileri gerekir. Depoları sayısı çok büyük olduğunda nerede toohave ipucu gereksinim toolook sonraki.

Veri modeli tanımlayan iki application Insights, bu sorunu toosolve alanlar: `request.source` ve `dependency.target`. Merhaba ilk alanı hello bağımlılık istek başlatılan hello bileşeni belirtir ve hello ikinci hello bağımlılık çağrının hello yanıt döndürdü hangi bileşenin tanımlar.


## <a name="example"></a>Örnek

Bir uygulama hisse SENEDİ hello geçerli Piyasa fiyatı hisse API adlı hello harici API kullanarak hisse senedi gösteren FİYATLAR örneği atalım. Merhaba hisse SENEDİ FİYATLARI uygulama sahip bir sayfa `Stock page` hello istemci web tarayıcısı kullanarak açılan `GET /Home/Stock`. Merhaba uygulama sorguları bir HTTP çağrısı kullanarak stok API hello `GET /api/stock/value`.

Bir sorgu çalıştırılarak elde edilen telemetri çözümleyebilirsiniz:

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

Tüm telemetri öğelerini hello kök paylaşma hello sonuç görünümü notta `operation_Id`. Ajax çağırdığınızda hello sayfasından - yeni benzersiz kimlik yapılan `qJSXU` atanan toohello bağımlılık telemetrisi olduğu ve sayfa görünümü'nın kimliği olarak kullanılan `operation_ParentId`. Sunucu isteği ajax'ın kimliği olarak sırayla kullanan `operation_ParentId`, vb..

| itemType   | ad                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| Sayfa görünümü   | Stok sayfası                |              | STYz               | STYz         |
| bağımlılık | GET /Home/stok           | qJSXU        | STYz               | STYz         |
| İstek    | GET Home/stok            | KqKwlrSt9PA = | qJSXU              | STYz         |
| bağımlılık | /Api/Stock/Value Al      | bBrf2L7mm2g = | KqKwlrSt9PA =       | STYz         |

Şimdi ne zaman hello çağrısı `GET /api/stock/value` tooan dış hizmet yapılan tooknow hello sunucu kimliğini istiyor. Böylece, ayarlayabilirsiniz `dependency.target` uygun şekilde alan. Merhaba dış hizmet izleme - desteklemediğinde `target` kümesinin toohello ana bilgisayar adı gibi hello hizmet `stock-prices-api.com`. Ancak bu hizmetin kendisi önceden tanımlanmış bir döndürerek tanımlarsa HTTP üstbilgisi - `target` hello hizmet hizmet telemetrisinden sorgulayarak Application Insights dağıtılmış toobuild izleme sağlayan bir kimlik içeriyor. 

## <a name="correlation-headers"></a>Bağıntı üstbilgileri

RFC teklif hello için üzerinde çalıştığımız [bağıntı HTTP Protokolü](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Bu teklif iki üstbilgi tanımlar:

- `Request-Id`Merhaba çağrı genel benzersiz kimliğini Hello Yürüt
- `Correlation-Context`-Dağıtılmış hello izleme özellikleri hello ad değer çiftleri koleksiyonu Yürüt

Merhaba standart iki şemaları, ayrıca tanımlar `Request-Id` oluşturma - düz ve hiyerarşik. Merhaba düz şemasıyla yoktur iyi bilinen `Id` hello için tanımlanmış anahtar `Correlation-Context` koleksiyonu.

Application Insights tanımlar hello [uzantısı](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) hello bağıntı HTTP protokolü için. Kullandığı `Request-Context` değer çiftleri hello anında arayanlar veya Aranan tarafından kullanılan özellikleri toopropagate hello koleksiyonu adlandırın. Application Insights SDK'sı kullanan bu başlığı tooset `dependency.target` ve `request.source` alanları.

## <a name="open-tracing-and-application-insights"></a>Açık izleme ve Application Insights

[İzleme açık](http://opentracing.io/) ve Application Insights veri modelleri görünüyor 

- `request`, `pageView` çok eşlemeleri**aralık** ile`span.kind = server`
- `dependency`çok eşlemeleri**aralık** ile`span.kind = client`
- `id`bir `request` ve `dependency` çok eşlemeleri**Span.Id**
- `operation_Id`çok eşlemeleri**TraceId**
- `operation_ParentId`çok eşlemeleri**başvuru** türü`ChileOf`

Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.

Bkz: [belirtimi](https://github.com/opentracing/specification/blob/master/specification.md) ve [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md) açık izleme kavramları tanımları için.


## <a name="telemetry-correlation-in-net"></a>.NET içinde telemetri bağıntı

Zaman içinde .NET yolları toocorrelate telemetri ve tanılama tanımlanan günlükleri. Yoktur `System.Diagnostics.CorrelationManager` tootrack izin vererek [LogicalOperationStack ve ActivityID](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`ve Windows ETW hello yöntemi tanımlayın [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger`kullanan [günlük kapsamları](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). WCF ve Http kablo "geçerli" bağlam yayma ayarlama.

Ancak bu yöntemleri otomatik dağıtılmış İzleme desteğini etkinleştirin alamadık. `DiagnosticsSource`bir şekilde toosupport makine bağıntı otomatik olarak yapılır. .NET kitaplıklarına tanılama kaynak desteklemek ve http gibi hello aktarım aracılığıyla hello bağıntı içeriğinin otomatik çapraz makine yayma sağlar.

Merhaba [Kılavuzu tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) tanılama kaynağında etkinlikleri izleme hello temellerini açıklar. 

Merhaba yeni etkinlik başlangıç ve ASP.NET Core 2.0 Http üstbilgilerinin ayıklama destekler. 

`System.Net.HttpClient`Başlangıç sürümünden `<fill in>` hello bağıntı Http üstbilgileri ve hello http çağrısı bir etkinlik olarak izleme otomatik yerleştirme destekler.

Yeni bir Http modülü yok [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) hello ASP.NET Klasik için. Bu modül telemetri bağıntı DiagnosticsSource kullanarak uygular. Gelen istek üstbilgileri göre etkinlik başlatır. Merhaba farklı istek işleme aşamalarını telemetrisinden hatalarla ilintilidir. Her IIS aşaması farklı Yönet iş parçacığı üzerinde çalıştığında bile hello örnekleridir.

Uygulama Insights SDK'sı başlangıç sürümü `2.4.0-beta1` DiagnosticsSource ve etkinlik toocollect telemetri kullanır ve hello geçerli etkinliği ile ilişkilendirin. 

## <a name="next-steps"></a>Sonraki adımlar

- [Özel telemetri yazın](app-insights-api-custom-events-metrics.md)
- Yerleşik mikro hizmetinizde Application Insights'ın tüm bileşenleri. Kullanıma [desteklenen platformlar](app-insights-platforms.md).
- Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- Nasıl çok öğrenin[genişletmek ve filtre telemetri](app-insights-api-filtering-sampling.md).
