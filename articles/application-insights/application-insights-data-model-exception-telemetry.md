---
title: "aaaAzure uygulama Insights Telemetri veri modeli - özel durum Telemetrisi | Microsoft Docs"
description: "Özel durum telemetrisi için uygulama Öngörüler veri modeli"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a>Özel durum telemetrisi: Application Insights veri modeli

İçinde [Application Insights](app-insights-overview.md), izlenen Merhaba uygulaması yürütülmesi sırasında oluşan bir işlenen veya işlenmeyen özel durum örneğini temsil eder.

## <a name="problem-id"></a>Sorun kimliği

Burada hello kodda özel durum oluştu tanımlayıcısı. Gruplandırma özel durumlar için kullanılır. Genellikle bir özel durum türü ve birleşimi bir işleve hello çağrı yığını.

En fazla uzunluk: 1024 karakter

## <a name="severity-level"></a>Önem düzeyi

Önem düzeyi izleme. Değeri olabilir `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="exception-details"></a>Özel durum ayrıntıları

(Genişletilmiş toobe)

## <a name="custom-properties"></a>Özel Özellikler

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Özel ölçümleri

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Sonraki adımlar

- Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- Nasıl çok öğrenin[web uygulamalarınızı Application Insights ile özel durumları tanılamak](app-insights-asp-net-exceptions.md).
- Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.
