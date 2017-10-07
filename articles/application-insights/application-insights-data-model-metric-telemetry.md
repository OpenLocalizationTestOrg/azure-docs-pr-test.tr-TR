---
title: "aaaAzure uygulama Insights Telemetri veri modeli - ölçüm Telemetri | Microsoft Docs"
description: "Ölçüm telemetri için uygulama Öngörüler veri modeli"
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
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>Ölçüm telemetri: Application Insights veri modeli

Ölçüm telemetri tarafından desteklenen iki tür vardır [Application Insights](app-insights-overview.md): tek ölçüm ve önceden toplanan ölçüm. Yalnızca bir ad ve değer bunun tek ölçüsüdür. Önceden toplanan ölçüm hello toplama aralığı ve standart sapmasını hello ölçüm minimum ve maksimum değerini belirtir.

Önceden toplanan ölçüm telemetri bu toplama süresi bir dakika olduğu varsayılır.

Application Insights tarafından desteklenen çeşitli iyi bilinen ölçüm adı vardır. 

Sistem ve işlem sayaçları temsil eden ölçüm:

| **.NET adı**             | **Platform belirsiz adı** | **REST API adı** | **Açıklama**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | İş sürüyor... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | Toplam makine CPU
| `\Memory\Available Bytes`                 | İş sürüyor... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | disk üzerindeki kullanılabilir bellek
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | İş sürüyor... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | Merhaba uygulaması barındıran hello işleminin CPU
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | İş sürüyor... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | Merhaba uygulama barındırma hello işlemi tarafından kullanılan bellek
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | İş sürüyor... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | Merhaba uygulama barındırma işlem tarafından g/ç işlemlerinin hızıdır. çalıştırır
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | İş sürüyor... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | uygulama tarafından işlenen istek oranı 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | İş sürüyor... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | uygulama tarafından oluşturulan özel durumları oranı
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | İş sürüyor... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | ortalama istek yürütme süresi
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | İş sürüyor... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | Bir kuyruktaki işleme hello bekleyen istek sayısı

## <a name="name"></a>Ad

Ad hello ölçüsü Application Insights portalı ve kullanıcı Arabirimi toosee istersiniz. 

## <a name="value"></a>Değer

Ölçüm için tek bir değer. Merhaba toplama için tek tek ölçüler toplamı.

## <a name="count"></a>Sayı

Merhaba ölçüm ağırlığı ölçüm birleştirilir. Ölçüm için ayarlanmamalıdır.

## <a name="min"></a>Min

En küçük değerini hello ölçüm birleştirilir. Ölçüm için ayarlanmamalıdır.

## <a name="max"></a>Maks.

En büyük değerini hello ölçüm birleştirilir. Ölçüm için ayarlanmamalıdır.

## <a name="standard-deviation"></a>Standart sapma

Merhaba standart sapmasını ölçüm birleştirilir. Ölçüm için ayarlanmamalıdır.

## <a name="custom-properties"></a>Özel Özellikler

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Sonraki adımlar

- Bilgi nasıl toouse [özel olayları ve ölçümleri için Application Insights API'si](app-insights-api-custom-events-metrics.md#trackmetric).
- Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.
