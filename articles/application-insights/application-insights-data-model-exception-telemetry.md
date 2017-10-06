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
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="d2158-103">Özel durum telemetrisi: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="d2158-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="d2158-104">İçinde [Application Insights](app-insights-overview.md), izlenen Merhaba uygulaması yürütülmesi sırasında oluşan bir işlenen veya işlenmeyen özel durum örneğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d2158-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="d2158-105">Sorun kimliği</span><span class="sxs-lookup"><span data-stu-id="d2158-105">Problem Id</span></span>

<span data-ttu-id="d2158-106">Burada hello kodda özel durum oluştu tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d2158-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="d2158-107">Gruplandırma özel durumlar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2158-107">Used for exceptions grouping.</span></span> <span data-ttu-id="d2158-108">Genellikle bir özel durum türü ve birleşimi bir işleve hello çağrı yığını.</span><span class="sxs-lookup"><span data-stu-id="d2158-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="d2158-109">En fazla uzunluk: 1024 karakter</span><span class="sxs-lookup"><span data-stu-id="d2158-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="d2158-110">Önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="d2158-110">Severity level</span></span>

<span data-ttu-id="d2158-111">Önem düzeyi izleme.</span><span class="sxs-lookup"><span data-stu-id="d2158-111">Trace severity level.</span></span> <span data-ttu-id="d2158-112">Değeri olabilir `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="d2158-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="d2158-113">Özel durum ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d2158-113">Exception details</span></span>

<span data-ttu-id="d2158-114">(Genişletilmiş toobe)</span><span class="sxs-lookup"><span data-stu-id="d2158-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="d2158-115">Özel Özellikler</span><span class="sxs-lookup"><span data-stu-id="d2158-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="d2158-116">Özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="d2158-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="d2158-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2158-117">Next steps</span></span>

- <span data-ttu-id="d2158-118">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="d2158-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="d2158-119">Nasıl çok öğrenin[web uygulamalarınızı Application Insights ile özel durumları tanılamak](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="d2158-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="d2158-120">Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d2158-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
