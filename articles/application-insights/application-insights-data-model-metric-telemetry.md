---
title: "Azure uygulama Insights Telemetri veri modeli - ölçüm Telemetri | Microsoft Docs"
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
ms.openlocfilehash: 42e55db4f932de85ee1a71c408b889e0ff9fe3e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="85d17-103">Ölçüm telemetri: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="85d17-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="85d17-104">Ölçüm telemetri tarafından desteklenen iki tür vardır [Application Insights](app-insights-overview.md): tek ölçüm ve önceden toplanan ölçüm.</span><span class="sxs-lookup"><span data-stu-id="85d17-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="85d17-105">Yalnızca bir ad ve değer bunun tek ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="85d17-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="85d17-106">Önceden toplanan ölçümü toplama aralığı ve standart sapmasını ölçüm minimum ve maksimum değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="85d17-106">Pre-aggregated metric specifies minimum and maximum value of the metric in the aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="85d17-107">Önceden toplanan ölçüm telemetri bu toplama süresi bir dakika olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="85d17-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="85d17-108">Application Insights tarafından desteklenen çeşitli iyi bilinen ölçüm adı vardır.</span><span class="sxs-lookup"><span data-stu-id="85d17-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="85d17-109">Sistem ve işlem sayaçları temsil eden ölçüm:</span><span class="sxs-lookup"><span data-stu-id="85d17-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="85d17-110">**.NET adı**</span><span class="sxs-lookup"><span data-stu-id="85d17-110">**.NET name**</span></span>             | <span data-ttu-id="85d17-111">**Platform belirsiz adı**</span><span class="sxs-lookup"><span data-stu-id="85d17-111">**Platform agnostic name**</span></span> | <span data-ttu-id="85d17-112">**REST API adı**</span><span class="sxs-lookup"><span data-stu-id="85d17-112">**REST API name**</span></span> | <span data-ttu-id="85d17-113">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="85d17-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="85d17-114">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-114">Work in progress...</span></span> | [<span data-ttu-id="85d17-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="85d17-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="85d17-116">Toplam makine CPU</span><span class="sxs-lookup"><span data-stu-id="85d17-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="85d17-117">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-117">Work in progress...</span></span> | [<span data-ttu-id="85d17-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="85d17-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="85d17-119">disk üzerindeki kullanılabilir bellek</span><span class="sxs-lookup"><span data-stu-id="85d17-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="85d17-120">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-120">Work in progress...</span></span> | [<span data-ttu-id="85d17-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="85d17-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="85d17-122">Uygulama barındırma işleminin CPU</span><span class="sxs-lookup"><span data-stu-id="85d17-122">CPU of the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="85d17-123">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-123">Work in progress...</span></span> | [<span data-ttu-id="85d17-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="85d17-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="85d17-125">Uygulama barındırma işlemi tarafından kullanılan bellek</span><span class="sxs-lookup"><span data-stu-id="85d17-125">memory used by the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="85d17-126">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-126">Work in progress...</span></span> | [<span data-ttu-id="85d17-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="85d17-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="85d17-128">Uygulama barındırma işlem tarafından g/ç işlemlerinin oranı çalıştırır</span><span class="sxs-lookup"><span data-stu-id="85d17-128">rate of I/O operations runs by process hosting the application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="85d17-129">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-129">Work in progress...</span></span> | [<span data-ttu-id="85d17-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="85d17-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="85d17-131">uygulama tarafından işlenen istek oranı</span><span class="sxs-lookup"><span data-stu-id="85d17-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="85d17-132">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-132">Work in progress...</span></span> | [<span data-ttu-id="85d17-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="85d17-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="85d17-134">uygulama tarafından oluşturulan özel durumları oranı</span><span class="sxs-lookup"><span data-stu-id="85d17-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="85d17-135">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-135">Work in progress...</span></span> | [<span data-ttu-id="85d17-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="85d17-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="85d17-137">ortalama istek yürütme süresi</span><span class="sxs-lookup"><span data-stu-id="85d17-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="85d17-138">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="85d17-138">Work in progress...</span></span> | [<span data-ttu-id="85d17-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="85d17-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="85d17-140">bir kuyruk işlemek için bekleyen istek sayısı</span><span class="sxs-lookup"><span data-stu-id="85d17-140">number of requests waiting for the processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="85d17-141">Ad</span><span class="sxs-lookup"><span data-stu-id="85d17-141">Name</span></span>

<span data-ttu-id="85d17-142">Application Insights portalı ve kullanıcı arabirimini görmek istediğiniz ölçüm adı.</span><span class="sxs-lookup"><span data-stu-id="85d17-142">Name of the metric you'd like to see in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="85d17-143">Değer</span><span class="sxs-lookup"><span data-stu-id="85d17-143">Value</span></span>

<span data-ttu-id="85d17-144">Ölçüm için tek bir değer.</span><span class="sxs-lookup"><span data-stu-id="85d17-144">Single value for measurement.</span></span> <span data-ttu-id="85d17-145">Toplama için tek tek ölçüler toplamı.</span><span class="sxs-lookup"><span data-stu-id="85d17-145">Sum of individual measurements for the aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="85d17-146">Sayı</span><span class="sxs-lookup"><span data-stu-id="85d17-146">Count</span></span>

<span data-ttu-id="85d17-147">Toplanan ölçüm ölçüm ağırlığı.</span><span class="sxs-lookup"><span data-stu-id="85d17-147">Metric weight of the aggregated metric.</span></span> <span data-ttu-id="85d17-148">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="85d17-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="85d17-149">Min</span><span class="sxs-lookup"><span data-stu-id="85d17-149">Min</span></span>

<span data-ttu-id="85d17-150">Toplanan ölçüm en küçük değeri.</span><span class="sxs-lookup"><span data-stu-id="85d17-150">Minimum value of the aggregated metric.</span></span> <span data-ttu-id="85d17-151">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="85d17-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="85d17-152">Maks.</span><span class="sxs-lookup"><span data-stu-id="85d17-152">Max</span></span>

<span data-ttu-id="85d17-153">Toplanan ölçüm maksimum değeri.</span><span class="sxs-lookup"><span data-stu-id="85d17-153">Maximum value of the aggregated metric.</span></span> <span data-ttu-id="85d17-154">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="85d17-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="85d17-155">Standart sapma</span><span class="sxs-lookup"><span data-stu-id="85d17-155">Standard deviation</span></span>

<span data-ttu-id="85d17-156">Toplanan ölçüm standart sapması.</span><span class="sxs-lookup"><span data-stu-id="85d17-156">Standard deviation of the aggregated metric.</span></span> <span data-ttu-id="85d17-157">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="85d17-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="85d17-158">Özel Özellikler</span><span class="sxs-lookup"><span data-stu-id="85d17-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="85d17-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85d17-159">Next steps</span></span>

- <span data-ttu-id="85d17-160">Nasıl kullanacağınızı öğrenin [özel olayları ve ölçümleri için Application Insights API'si](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="85d17-160">Learn how to use [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="85d17-161">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="85d17-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="85d17-162">Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="85d17-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
