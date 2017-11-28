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
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="7367d-103">Telemetri izleme: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="7367d-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="7367d-104">İzleme telemetri (içinde [Application Insights](app-insights-overview.md)) temsil eden `printf` stili metin arama izleme deyimleri.</span><span class="sxs-lookup"><span data-stu-id="7367d-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="7367d-105">`Log4Net`, `NLog`, ve diğer metin tabanlı günlük dosyası girişlerini, bu türdeki örneklerin dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="7367d-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="7367d-106">Merhaba izleme ölçümler bir genişletilebilirlik yok.</span><span class="sxs-lookup"><span data-stu-id="7367d-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="7367d-107">İleti</span><span class="sxs-lookup"><span data-stu-id="7367d-107">Message</span></span>

<span data-ttu-id="7367d-108">İzleme iletisi.</span><span class="sxs-lookup"><span data-stu-id="7367d-108">Trace message.</span></span>

<span data-ttu-id="7367d-109">En fazla uzunluk: 32768 karakterleri</span><span class="sxs-lookup"><span data-stu-id="7367d-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="7367d-110">Önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="7367d-110">Severity level</span></span>

<span data-ttu-id="7367d-111">Önem düzeyi izleme.</span><span class="sxs-lookup"><span data-stu-id="7367d-111">Trace severity level.</span></span> <span data-ttu-id="7367d-112">Değeri olabilir `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="7367d-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="7367d-113">Özel Özellikler</span><span class="sxs-lookup"><span data-stu-id="7367d-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="7367d-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7367d-114">Next steps</span></span>

- <span data-ttu-id="7367d-115">[Application ınsights'ta .NET izleme günlükleri keşfedin](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7367d-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="7367d-116">[İzleme günlüklerini Application Insights'ta Java keşfedin](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7367d-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="7367d-117">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="7367d-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="7367d-118">Özel İzleme telemetri yazma</span><span class="sxs-lookup"><span data-stu-id="7367d-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="7367d-119">Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7367d-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
