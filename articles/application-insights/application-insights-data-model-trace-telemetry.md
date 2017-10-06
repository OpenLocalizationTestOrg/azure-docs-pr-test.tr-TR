---
title: aaaAzure uygulama Insights Telemetri veri modeli - izleme Telemetri | Microsoft Docs
description: "İzleme telemetri için uygulama Öngörüler veri modeli"
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a>Telemetri izleme: Application Insights veri modeli

İzleme telemetri (içinde [Application Insights](app-insights-overview.md)) temsil eden `printf` stili metin arama izleme deyimleri. `Log4Net`, `NLog`, ve diğer metin tabanlı günlük dosyası girişlerini, bu türdeki örneklerin dönüştürülür. Merhaba izleme ölçümler bir genişletilebilirlik yok.

## <a name="message"></a>İleti

İzleme iletisi.

En fazla uzunluk: 32768 karakterleri

## <a name="severity-level"></a>Önem düzeyi

Önem düzeyi izleme. Değeri olabilir `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="custom-properties"></a>Özel Özellikler

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Sonraki adımlar

- [Application ınsights'ta .NET izleme günlükleri keşfedin](app-insights-asp-net-trace-logs.md).
- [İzleme günlüklerini Application Insights'ta Java keşfedin](app-insights-java-trace-logs.md).
- Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- [Özel İzleme telemetri yazma](app-insights-api-custom-events-metrics.md#tracktrace)
- Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.
