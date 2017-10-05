---
title: "Azure uygulama Insights Telemetri veri modeli - özel durum Telemetrisi | Microsoft Docs"
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="b483b-103">Özel durum telemetrisi: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="b483b-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="b483b-104">İçinde [Application Insights](app-insights-overview.md), izlenen uygulama yürütülmesi sırasında oluşan bir işlenen veya işlenmeyen özel durum örneğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b483b-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="b483b-105">Sorun kimliği</span><span class="sxs-lookup"><span data-stu-id="b483b-105">Problem Id</span></span>

<span data-ttu-id="b483b-106">Burada kodda özel durum oluştu tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b483b-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="b483b-107">Gruplandırma özel durumlar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b483b-107">Used for exceptions grouping.</span></span> <span data-ttu-id="b483b-108">Genellikle bir özel durum türü ve birleşimi bir işleve çağrı yığını.</span><span class="sxs-lookup"><span data-stu-id="b483b-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="b483b-109">En fazla uzunluk: 1024 karakter</span><span class="sxs-lookup"><span data-stu-id="b483b-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="b483b-110">Önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="b483b-110">Severity level</span></span>

<span data-ttu-id="b483b-111">Önem düzeyi izleme.</span><span class="sxs-lookup"><span data-stu-id="b483b-111">Trace severity level.</span></span> <span data-ttu-id="b483b-112">Değeri olabilir `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="b483b-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="b483b-113">Özel durum ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b483b-113">Exception details</span></span>

<span data-ttu-id="b483b-114">(Genişletilmesi için)</span><span class="sxs-lookup"><span data-stu-id="b483b-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="b483b-115">Özel Özellikler</span><span class="sxs-lookup"><span data-stu-id="b483b-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="b483b-116">Özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="b483b-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="b483b-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b483b-117">Next steps</span></span>

- <span data-ttu-id="b483b-118">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="b483b-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="b483b-119">Bilgi edinmek için nasıl [web uygulamalarınızı Application Insights ile özel durumları tanılamak](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="b483b-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="b483b-120">Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b483b-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
