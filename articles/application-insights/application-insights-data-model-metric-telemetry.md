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
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="cdc8f-103">Ölçüm telemetri: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="cdc8f-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="cdc8f-104">Ölçüm telemetri tarafından desteklenen iki tür vardır [Application Insights](app-insights-overview.md): tek ölçüm ve önceden toplanan ölçüm.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="cdc8f-105">Yalnızca bir ad ve değer bunun tek ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="cdc8f-106">Önceden toplanan ölçüm hello toplama aralığı ve standart sapmasını hello ölçüm minimum ve maksimum değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="cdc8f-107">Önceden toplanan ölçüm telemetri bu toplama süresi bir dakika olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="cdc8f-108">Application Insights tarafından desteklenen çeşitli iyi bilinen ölçüm adı vardır.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="cdc8f-109">Sistem ve işlem sayaçları temsil eden ölçüm:</span><span class="sxs-lookup"><span data-stu-id="cdc8f-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="cdc8f-110">**.NET adı**</span><span class="sxs-lookup"><span data-stu-id="cdc8f-110">**.NET name**</span></span>             | <span data-ttu-id="cdc8f-111">**Platform belirsiz adı**</span><span class="sxs-lookup"><span data-stu-id="cdc8f-111">**Platform agnostic name**</span></span> | <span data-ttu-id="cdc8f-112">**REST API adı**</span><span class="sxs-lookup"><span data-stu-id="cdc8f-112">**REST API name**</span></span> | <span data-ttu-id="cdc8f-113">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="cdc8f-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="cdc8f-114">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-114">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="cdc8f-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="cdc8f-116">Toplam makine CPU</span><span class="sxs-lookup"><span data-stu-id="cdc8f-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="cdc8f-117">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-117">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="cdc8f-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="cdc8f-119">disk üzerindeki kullanılabilir bellek</span><span class="sxs-lookup"><span data-stu-id="cdc8f-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="cdc8f-120">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-120">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="cdc8f-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="cdc8f-122">Merhaba uygulaması barındıran hello işleminin CPU</span><span class="sxs-lookup"><span data-stu-id="cdc8f-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="cdc8f-123">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-123">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="cdc8f-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="cdc8f-125">Merhaba uygulama barındırma hello işlemi tarafından kullanılan bellek</span><span class="sxs-lookup"><span data-stu-id="cdc8f-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="cdc8f-126">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-126">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="cdc8f-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="cdc8f-128">Merhaba uygulama barındırma işlem tarafından g/ç işlemlerinin hızıdır. çalıştırır</span><span class="sxs-lookup"><span data-stu-id="cdc8f-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="cdc8f-129">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-129">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="cdc8f-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="cdc8f-131">uygulama tarafından işlenen istek oranı</span><span class="sxs-lookup"><span data-stu-id="cdc8f-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="cdc8f-132">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-132">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="cdc8f-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="cdc8f-134">uygulama tarafından oluşturulan özel durumları oranı</span><span class="sxs-lookup"><span data-stu-id="cdc8f-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="cdc8f-135">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-135">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="cdc8f-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="cdc8f-137">ortalama istek yürütme süresi</span><span class="sxs-lookup"><span data-stu-id="cdc8f-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="cdc8f-138">İş sürüyor...</span><span class="sxs-lookup"><span data-stu-id="cdc8f-138">Work in progress...</span></span> | [<span data-ttu-id="cdc8f-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="cdc8f-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="cdc8f-140">Bir kuyruktaki işleme hello bekleyen istek sayısı</span><span class="sxs-lookup"><span data-stu-id="cdc8f-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="cdc8f-141">Ad</span><span class="sxs-lookup"><span data-stu-id="cdc8f-141">Name</span></span>

<span data-ttu-id="cdc8f-142">Ad hello ölçüsü Application Insights portalı ve kullanıcı Arabirimi toosee istersiniz.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="cdc8f-143">Değer</span><span class="sxs-lookup"><span data-stu-id="cdc8f-143">Value</span></span>

<span data-ttu-id="cdc8f-144">Ölçüm için tek bir değer.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-144">Single value for measurement.</span></span> <span data-ttu-id="cdc8f-145">Merhaba toplama için tek tek ölçüler toplamı.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="cdc8f-146">Sayı</span><span class="sxs-lookup"><span data-stu-id="cdc8f-146">Count</span></span>

<span data-ttu-id="cdc8f-147">Merhaba ölçüm ağırlığı ölçüm birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="cdc8f-148">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="cdc8f-149">Min</span><span class="sxs-lookup"><span data-stu-id="cdc8f-149">Min</span></span>

<span data-ttu-id="cdc8f-150">En küçük değerini hello ölçüm birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="cdc8f-151">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="cdc8f-152">Maks.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-152">Max</span></span>

<span data-ttu-id="cdc8f-153">En büyük değerini hello ölçüm birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="cdc8f-154">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="cdc8f-155">Standart sapma</span><span class="sxs-lookup"><span data-stu-id="cdc8f-155">Standard deviation</span></span>

<span data-ttu-id="cdc8f-156">Merhaba standart sapmasını ölçüm birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="cdc8f-157">Ölçüm için ayarlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="cdc8f-158">Özel Özellikler</span><span class="sxs-lookup"><span data-stu-id="cdc8f-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="cdc8f-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cdc8f-159">Next steps</span></span>

- <span data-ttu-id="cdc8f-160">Bilgi nasıl toouse [özel olayları ve ölçümleri için Application Insights API'si](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="cdc8f-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="cdc8f-161">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="cdc8f-162">Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cdc8f-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
