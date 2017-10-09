---
title: aaaAzure uygulama Insights Telemetri veri modeli - olay Telemetri | Microsoft Docs
description: "Olay telemetri için uygulama Öngörüler veri modeli"
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>Olay telemetri: Application Insights veri modeli

Telemetri öğeleri olay oluşturabilirsiniz (içinde [Application Insights](app-insights-overview.md)) toorepresent, uygulamanızda gerçekleşen bir olay. Genellikle düğmesini tıklatın veya satın alma siparişi gibi bir kullanıcı etkileşimi değil. Ayrıca, uygulama yaşam döngüsü olay başlatma veya yapılandırma güncelleştirme gibi de olabilir. 

Anlam olarak, olaylar olabilir veya bağlantılı toorequests olmayabilir. Ancak, düzgün kullandıysanız, olay telemetri istekleri veya izlemeleri daha önemlidir. Olayları iş telemetri temsil eder ve daha az agresif konu tooseparate olmalıdır [örnekleme](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Ad

Olay adı. tooallow uygun gruplandırma ve yararlı ölçümler, böylece ayrı olay adları az sayıda oluşturur, uygulamanızın kısıtlayın. Örneğin, bir olay oluşturulan her örneği için ayrı bir ad kullanmayın.

En fazla uzunluk: 512 karakteri

## <a name="custom-properties"></a>Özel Özellikler

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Özel ölçümleri

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Sonraki adımlar

- Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- [Özel olay telemetri yazma](app-insights-api-custom-events-metrics.md#trackevent)
- Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.
