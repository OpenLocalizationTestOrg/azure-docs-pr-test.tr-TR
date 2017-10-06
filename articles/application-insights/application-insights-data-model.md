---
title: aaaAzure uygulama Insights Telemetri veri modeli | Microsoft Docs
description: "Uygulama Öngörüler veri modeline genel bakış"
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
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Uygulama Insights telemetri veri modeli

[Azure Application Insights](app-insights-overview.md) hello performans ve uygulamanızın kullanımını analiz etme, web uygulama toohello Azure portal, telemetri gönderir. Böylece olası toocreate platform ve dilden bağımsız izleme olur hello telemetri modeli standartlaştırılmıştır. 

Application Insights tarafından toplanan verileri bu genel uygulama yürütme desen modelleri:

![Uygulama Öngörüler uygulama modeli](./media/application-insights-data-model/application-insights-data-model.png)

Merhaba aşağıdaki telemetri kullanılan toomonitor hello uygulamanızın yürütülmesini türleridir. Merhaba aşağıdaki üç tür genellikle otomatik olarak hello Application Insights SDK'sı tarafından hello web uygulama çerçevesinden toplanır:

* [**İstek** ](application-insights-data-model-request-telemetry.md) -toolog bir isteği alındı, uygulamanız tarafından oluşturulan. Örneğin, hello Application Insights web SDK'sı web uygulamanızı alır her HTTP isteği için bir istek telemetri öğesi otomatik olarak oluşturur. 

    Bir **işlemi** bir isteği işler yürütme hello iş parçacıklarının sayısıdır. Ayrıca [kod yazmayı](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor işlemi, diğer türleri gibi bir "uyandırmak" bir web işi ya da, düzenli aralıklarla işlev verilerini işler.  Her bir işlemin bir kimliği vardır. Uygulamanızı hello isteği işlerken kullanılan too[group]((application-insights-correlation.md) olabilir bu kimliği tüm telemetri oluşturulur. Her işlem ya da başarılı veya başarısız olur ve bir süre vardır.
* [**Özel durum** ](application-insights-data-model-exception-telemetry.md) -genellikle bir işlemi toofail neden olan bir özel durumu temsil eder.
* [**Bağımlılık** ](application-insights-data-model-dependency-telemetry.md) -uygulama tooan dış hizmeti veya bir REST API veya SQL gibi depolama bir çağrısını temsil eder. ASP.NET, bağımlılık çağrıları tooSQL tarafından tanımlanan `System.Data`. Çağrıları tooHTTP uç noktaları tarafından tanımlanan `System.Net`. 

Application Insights üç ek veri türleri için özel telemetri sağlar:

* [İzleme](application-insights-data-model-trace-telemetry.md) - ya da doğrudan kullanılan veya bir bağdaştırıcı tooimplement tanılama günlükleri aracılığıyla tanıdık tooyou olduğu gibi bir izleme çerçevesini kullanarak `Log4Net` veya `System.Diagnostics`.
* [Olay](application-insights-data-model-event-telemetry.md) -genellikle, toocapture kullanıcı etkileşimi tooanalyze kullanım desenlerini hizmetiniz ile kullanılır.
* [Ölçüm](application-insights-data-model-metric-telemetry.md) -tooreport düzenli skaler ölçümleri kullanılır.

Her telemetri öğesi hello tanımlayabilirsiniz [bağlam bilgilerini](application-insights-data-model-context.md) uygulama sürümü ya da kullanıcı oturum kimliği gibi. Bağlam belirli senaryolar engelini kaldırır kesin türü belirtilmiş alanları kümesidir. Uygulama sürümü düzgün başlatılmadı, Application Insights yeni desenleri çözümünüzün yeniden dağıtımını ile ilişkili uygulama davranış algılayabilir. Oturum kimliği kullanılan toocalculate hello kesintisi veya kullanıcılar üzerinde sorunu etkisi olabilir. Oturum kimliği değerlerin ayrı sayım belirli hesaplama bağımlılık başarısız oldu, hata izleme veya kritik bir özel durumla bir etkisi iyi anlamış sağlar.

Application Insights telemetri modeli tanımlayan bir yol çok[bağıntısını](application-insights-correlation.md) bir parçası olmasından telemetri toohello işlemi. Örneğin, bir istek bir SQL veritabanı çağrılarını yapabilirsiniz ve tanılama bilgileri kaydedilir. Merhaba bağıntı bağlamı geri toohello isteği telemetri bağlamanın telemetriyi öğeleri için ayarlayabilirsiniz.

## <a name="schema-improvements"></a>Şema geliştirmeleri

Uygulama Öngörüler veri modelini basit ve basit ancak güçlü bir şekilde toomodel uygulama telemetrinizi olduğu. Biz tookeep hello modeli basit ve ince toosupport önemli senaryoları çaba ve Gelişmiş kullanım için tooextend hello şeması izin verir.

tooreport veri modelini veya şema sorunları ve önerileri kullanın GitHub [Applicationınsights giriş](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) deposu.

## <a name="next-steps"></a>Sonraki adımlar

- [Özel telemetri yazın](app-insights-api-custom-events-metrics.md)
- Nasıl çok öğrenin[genişletmek ve filtre telemetri](app-insights-api-filtering-sampling.md).
- Kullanım [örnekleme](app-insights-sampling.md) telemetri toominimize miktarı veri modelini temel alarak.
- Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.
