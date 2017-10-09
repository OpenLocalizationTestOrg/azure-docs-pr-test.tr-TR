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
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="7030d-103">Olay telemetri: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="7030d-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="7030d-104">Telemetri öğeleri olay oluşturabilirsiniz (içinde [Application Insights](app-insights-overview.md)) toorepresent, uygulamanızda gerçekleşen bir olay.</span><span class="sxs-lookup"><span data-stu-id="7030d-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="7030d-105">Genellikle düğmesini tıklatın veya satın alma siparişi gibi bir kullanıcı etkileşimi değil.</span><span class="sxs-lookup"><span data-stu-id="7030d-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="7030d-106">Ayrıca, uygulama yaşam döngüsü olay başlatma veya yapılandırma güncelleştirme gibi de olabilir.</span><span class="sxs-lookup"><span data-stu-id="7030d-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="7030d-107">Anlam olarak, olaylar olabilir veya bağlantılı toorequests olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="7030d-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="7030d-108">Ancak, düzgün kullandıysanız, olay telemetri istekleri veya izlemeleri daha önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7030d-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="7030d-109">Olayları iş telemetri temsil eder ve daha az agresif konu tooseparate olmalıdır [örnekleme](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="7030d-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="7030d-110">Ad</span><span class="sxs-lookup"><span data-stu-id="7030d-110">Name</span></span>

<span data-ttu-id="7030d-111">Olay adı.</span><span class="sxs-lookup"><span data-stu-id="7030d-111">Event name.</span></span> <span data-ttu-id="7030d-112">tooallow uygun gruplandırma ve yararlı ölçümler, böylece ayrı olay adları az sayıda oluşturur, uygulamanızın kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="7030d-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="7030d-113">Örneğin, bir olay oluşturulan her örneği için ayrı bir ad kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7030d-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="7030d-114">En fazla uzunluk: 512 karakteri</span><span class="sxs-lookup"><span data-stu-id="7030d-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="7030d-115">Özel Özellikler</span><span class="sxs-lookup"><span data-stu-id="7030d-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="7030d-116">Özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="7030d-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="7030d-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7030d-117">Next steps</span></span>

- <span data-ttu-id="7030d-118">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="7030d-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="7030d-119">Özel olay telemetri yazma</span><span class="sxs-lookup"><span data-stu-id="7030d-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="7030d-120">Kullanıma [platformları](app-insights-platforms.md) Application Insights tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7030d-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
