---
title: "bir olay kaynağı tooyour Azure zaman serisi Öngörüler ortam aaaAdd | Microsoft Docs"
description: "Bu öğreticide, bir olay kaynağı tooyour zaman serisi Öngörüler ortama bağlanma"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="9b675-103">Merhaba Ibiza portalını kullanarak, zaman serisi Öngörüler ortamınız için bir olay kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9b675-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="9b675-104">Zaman Serisi Görüşleri Olay Kaynağı, Azure Event Hubs gibi bir olay aracısından türetilir.</span><span class="sxs-lookup"><span data-stu-id="9b675-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="9b675-105">Zaman serisi Öngörüler tooEvent kaynakları, kullanıcıların toowrite tek satırlık bir kod gerek kalmadan hello veri akışı alma doğrudan bağlanır.</span><span class="sxs-lookup"><span data-stu-id="9b675-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="9b675-106">Şu anda Zaman Serisi Görüşleri, Azure Event Hubs'ı ve Azure IoT Hub'larını destekler.</span><span class="sxs-lookup"><span data-stu-id="9b675-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="9b675-107">Hello gelecekteki, daha fazla olay kaynakları eklenir.</span><span class="sxs-lookup"><span data-stu-id="9b675-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="9b675-108">Adımları tooadd bir olay kaynağı tooyour ortamı</span><span class="sxs-lookup"><span data-stu-id="9b675-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="9b675-109">İçinde toohello oturum [Ibiza portalını](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b675-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="9b675-110">"Tüm kaynaklar" Merhaba Ibiza portalında sol tarafındaki hello hello menüsünde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9b675-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="9b675-111">Zaman Serisi Görüşleri ortamınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="9b675-111">Select your Time Series Insights environment.</span></span>

  ![Merhaba zaman serisi Öngörüler olay kaynağı oluşturma](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="9b675-113">“Olay Kaynakları” öğesini seçin ve “+ Ekle” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9b675-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Merhaba zaman serisi Öngörüler olay kaynağı - Ayrıntılar](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="9b675-115">Merhaba hello olay kaynağı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9b675-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="9b675-116">Bu ad, bu olay kaynağından gelen tüm olaylarla ilişkilendirilmiştir ve sorgu zamanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9b675-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="9b675-117">Olay hub'ı kaynakların hello geçerli abonelikte hello listeden bir olay hub'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9b675-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="9b675-118">Aksi takdirde içeri aktarma seçeneği "sağla olay hub'ı ayarlarını el ile" toospecify bir event hub'ında başka bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="9b675-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="9b675-119">Olayların JSON biçiminde yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b675-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="9b675-120">Okuma izni hello event hub'ındaki ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9b675-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="9b675-121">Olay hub’ı tüketici grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="9b675-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9b675-122">Bu tüketici grubunun başka hiçbir hizmet (örneğin, Stream Analytics işi veya başka bir Zaman Serisi Görüşleri ortamı) tarafından kullanılmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9b675-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="9b675-123">Bir tüketici grubundaki diğer hizmetler tarafından kullanılıyorsa, işlem olumsuz bu ortam için etkilenen okuyun ve diğer hizmetleri hello.</span><span class="sxs-lookup"><span data-stu-id="9b675-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="9b675-124">"$Default" Merhaba tüketici grubu olarak kullanıyorsanız, diğer okuyucular tarafından toopotential yeniden yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="9b675-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="9b675-125">“Oluştur” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9b675-125">Click “Create.”</span></span>

<span data-ttu-id="9b675-126">Merhaba olay kaynağı oluşturulduktan sonra zaman serisi Öngörüler ortamınıza veri akış otomatik olarak başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="9b675-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b675-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9b675-127">Next steps</span></span>

* <span data-ttu-id="9b675-128">[Olayları göndermek](time-series-insights-send-events.md) toohello olay kaynağı</span><span class="sxs-lookup"><span data-stu-id="9b675-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="9b675-129">[Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9b675-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
