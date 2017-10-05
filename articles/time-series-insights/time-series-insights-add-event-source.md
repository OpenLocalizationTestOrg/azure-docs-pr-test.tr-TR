---
title: "Azure Zaman Serisi Görüşleri ortamınıza olay kaynağı ekleme | Microsoft Docs"
description: "Bu öğreticide, Zaman Serisi Görüşleri ortamınıza bir olay kaynağı bağlayacaksınız"
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
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="f327a-103">Ibiza portalını kullanarak Zaman Serisi Görüşleri ortamınız için olay kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f327a-103">Create an event source for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="f327a-104">Zaman Serisi Görüşleri Olay Kaynağı, Azure Event Hubs gibi bir olay aracısından türetilir.</span><span class="sxs-lookup"><span data-stu-id="f327a-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="f327a-105">Zaman Serisi Görüşleri doğrudan Olay Kaynaklarına bağlanarak, kullanıcının tek bir kod satırı bile yazmasına gerek kalmadan veri akışını alır.</span><span class="sxs-lookup"><span data-stu-id="f327a-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="f327a-106">Şu anda Zaman Serisi Görüşleri, Azure Event Hubs'ı ve Azure IoT Hub'larını destekler.</span><span class="sxs-lookup"><span data-stu-id="f327a-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="f327a-107">İleride daha fazla Olay Kaynağı eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="f327a-107">In the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="f327a-108">Ortamınıza olay kaynağı ekleme adımları</span><span class="sxs-lookup"><span data-stu-id="f327a-108">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="f327a-109">[Ibiza portalında](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f327a-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="f327a-110">Ibiza portalının sol tarafındaki menüde bulunan "Tüm kaynaklar" seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f327a-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3.  <span data-ttu-id="f327a-111">Zaman Serisi Görüşleri ortamınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="f327a-111">Select your Time Series Insights environment.</span></span>

  ![Zaman Serisi Görüşleri oluşturma olay kaynağı](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="f327a-113">“Olay Kaynakları” öğesini seçin ve “+ Ekle” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f327a-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Zaman Serisi Görüşleri oluşturma olay kaynağı - ayrıntılar](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="f327a-115">Olay kaynağının adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="f327a-115">Specify the name of the event source.</span></span> <span data-ttu-id="f327a-116">Bu ad, bu olay kaynağından gelen tüm olaylarla ilişkilendirilmiştir ve sorgu zamanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f327a-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="f327a-117">Geçerli abonelikte yer alan Olay Hub'ı kaynakları listesinden bir olay hub'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f327a-117">Select an event hub from the list of Event Hub resources in the current subscription.</span></span> <span data-ttu-id="f327a-118">Alternatif olarak, başka bir abonelikte yer alan bir olay hub'ı belirtmek için "Olay hub'ı ayarlarını elle gir" içeri aktarma seçeneğini de belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f327a-118">Otherwise choose import option "Provide Event Hub settings manually” to specify an event hub in another subscription.</span></span> <span data-ttu-id="f327a-119">Olayların JSON biçiminde yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f327a-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="f327a-120">Olay hub’ında okuma izni olan ilkeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="f327a-120">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="f327a-121">Olay hub’ı tüketici grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="f327a-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f327a-122">Bu tüketici grubunun başka hiçbir hizmet (örneğin, Stream Analytics işi veya başka bir Zaman Serisi Görüşleri ortamı) tarafından kullanılmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f327a-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="f327a-123">Tüketici grubu başka hizmetler tarafından kullanılıyorsa, bu ortam ve diğer hizmetler için okuma işlemi olumsuz etkilenir.</span><span class="sxs-lookup"><span data-stu-id="f327a-123">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="f327a-124">Tüketici grubu olarak “$Default” kullanıyorsanız, bu diğer okuyucular tarafından olası yeniden kullanıma yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="f327a-124">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

9.  <span data-ttu-id="f327a-125">“Oluştur” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f327a-125">Click “Create.”</span></span>

<span data-ttu-id="f327a-126">Olay kaynağının oluşturulmasından sonra, Zaman Serisi Görüşleri ortamınıza veri akışını otomatik olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="f327a-126">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f327a-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f327a-127">Next steps</span></span>

* <span data-ttu-id="f327a-128">Olay kaynağına [olayları gönderme](time-series-insights-send-events.md)</span><span class="sxs-lookup"><span data-stu-id="f327a-128">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="f327a-129">[Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f327a-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
