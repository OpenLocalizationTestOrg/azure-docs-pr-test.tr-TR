---
title: "aaaAzure uygulama Insights Telemetri veri modeli - bağımlılık Telemetrisi | Microsoft Docs"
description: "Bağımlılık telemetrisi için uygulama Öngörüler veri modeli"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="c8f20-103">Bağımlılık telemetrisi: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="c8f20-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="c8f20-104">Bağımlılık Telemetrisi (içinde [Application Insights](app-insights-overview.md)) hello izlenen bileşenin SQL ya da bir HTTP uç noktası gibi uzak bir bileşeni ile etkileşim temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c8f20-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="c8f20-105">Ad</span><span class="sxs-lookup"><span data-stu-id="c8f20-105">Name</span></span>

<span data-ttu-id="c8f20-106">Bu bağımlılık çağrısı ile başlatılan hello komut adı.</span><span class="sxs-lookup"><span data-stu-id="c8f20-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="c8f20-107">Düşük önem düzeyi değeri.</span><span class="sxs-lookup"><span data-stu-id="c8f20-107">Low cardinality value.</span></span> <span data-ttu-id="c8f20-108">Saklı yordam adı ve URL yolu şablonunu örnektir.</span><span class="sxs-lookup"><span data-stu-id="c8f20-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="c8f20-109">Kimlik</span><span class="sxs-lookup"><span data-stu-id="c8f20-109">ID</span></span>

<span data-ttu-id="c8f20-110">Bir bağımlılık çağrısı örneği tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c8f20-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="c8f20-111">Bağıntı için hello istek telemetri öğesi toothis bağımlılık çağrısı karşılık gelen ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f20-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="c8f20-112">Daha fazla bilgi için bkz: [bağıntı](application-insights-correlation.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="c8f20-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="c8f20-113">Veriler</span><span class="sxs-lookup"><span data-stu-id="c8f20-113">Data</span></span>

<span data-ttu-id="c8f20-114">Bu bağımlılık çağrısı tarafından başlatılan komutu.</span><span class="sxs-lookup"><span data-stu-id="c8f20-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="c8f20-115">SQL deyimi ve HTTP URL içeren tüm sorgu parametrelerini örnektir.</span><span class="sxs-lookup"><span data-stu-id="c8f20-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="c8f20-116">Tür</span><span class="sxs-lookup"><span data-stu-id="c8f20-116">Type</span></span>

<span data-ttu-id="c8f20-117">Bağımlılık türü adı.</span><span class="sxs-lookup"><span data-stu-id="c8f20-117">Dependency type name.</span></span> <span data-ttu-id="c8f20-118">Bağımlılıklar mantıksal gruplandırmasını ve commandName ve resultCode gibi diğer alanlar yorumu düşük önem düzeyi değeri.</span><span class="sxs-lookup"><span data-stu-id="c8f20-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="c8f20-119">SQL Azure tablo ve HTTP örnektir.</span><span class="sxs-lookup"><span data-stu-id="c8f20-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="c8f20-120">Hedef</span><span class="sxs-lookup"><span data-stu-id="c8f20-120">Target</span></span>

<span data-ttu-id="c8f20-121">Hedef site bağımlılık çağrısı.</span><span class="sxs-lookup"><span data-stu-id="c8f20-121">Target site of a dependency call.</span></span> <span data-ttu-id="c8f20-122">Sunucu adı, ana bilgisayar adresi olarak gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="c8f20-122">Examples are server name, host address.</span></span> <span data-ttu-id="c8f20-123">Daha fazla bilgi için bkz: [bağıntı](application-insights-correlation.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="c8f20-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="c8f20-124">Süre</span><span class="sxs-lookup"><span data-stu-id="c8f20-124">Duration</span></span>

<span data-ttu-id="c8f20-125">Süre biçimde istek: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="c8f20-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="c8f20-126">Olmalıdır değerinden `1000` gün.</span><span class="sxs-lookup"><span data-stu-id="c8f20-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="c8f20-127">Sonuç kodu</span><span class="sxs-lookup"><span data-stu-id="c8f20-127">Result code</span></span>

<span data-ttu-id="c8f20-128">Bir bağımlılık araması Sonuç kodu.</span><span class="sxs-lookup"><span data-stu-id="c8f20-128">Result code of a dependency call.</span></span> <span data-ttu-id="c8f20-129">SQL hata kodu ve HTTP durum kodu örnektir.</span><span class="sxs-lookup"><span data-stu-id="c8f20-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="c8f20-130">Başarılı</span><span class="sxs-lookup"><span data-stu-id="c8f20-130">Success</span></span>

<span data-ttu-id="c8f20-131">Başarılı veya başarısız çağrının gösterimi.</span><span class="sxs-lookup"><span data-stu-id="c8f20-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="c8f20-132">Özel Özellikler</span><span class="sxs-lookup"><span data-stu-id="c8f20-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="c8f20-133">Özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="c8f20-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="c8f20-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8f20-134">Next steps</span></span>

- <span data-ttu-id="c8f20-135">Bağımlılık izleme ayarlama [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="c8f20-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="c8f20-136">Bağımlılık izleme ayarlama [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="c8f20-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="c8f20-137">Özel bağımlılık telemetrisi yazma</span><span class="sxs-lookup"><span data-stu-id="c8f20-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="c8f20-138">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="c8f20-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="c8f20-139">Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8f20-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
