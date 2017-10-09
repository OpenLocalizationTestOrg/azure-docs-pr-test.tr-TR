---
title: "aaaAdd başvuru veri kümesi tooyour Azure zaman serisi Öngörüler ortamı | Microsoft Docs"
description: "Bu öğreticide, başvuru veri kümesi tooyour zaman serisi Öngörüler ortam Ekle"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="1c8bc-103">Merhaba Ibiza portalını kullanarak, zaman serisi Öngörüler ortamınız için bir başvuru veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c8bc-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="1c8bc-104">Bir başvuru veri kümesi, olay kaynağınızdan hello olaylarla engagement'ta öğeleri koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="1c8bc-105">Zaman Serisi Görüşleri giriş altyapısı, olay kaynağınızdaki bir olay ile başvuru veri kümenizdeki bir öğeyi birleştirir.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="1c8bc-106">Bu genişletilmiş olay daha sonra sorgu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-106">This augmented event is then available for query.</span></span> <span data-ttu-id="1c8bc-107">Bu katılımı hello tuşları başvuru veri kümesinde tanımlanan temel alır.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="1c8bc-108">Adımları tooadd bir başvuru veri kümesi tooyour ortamı</span><span class="sxs-lookup"><span data-stu-id="1c8bc-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="1c8bc-109">İçinde toohello oturum [Ibiza portalını](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c8bc-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c8bc-110">"Tüm kaynaklar" Merhaba Ibiza portalında sol tarafındaki hello hello menüsünde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="1c8bc-111">Zaman Serisi Görüşleri ortamınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-111">Select your Time Series Insights environment.</span></span>

    ![Merhaba zaman serisi Öngörüler başvuru veri kümesi oluşturma](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="1c8bc-113">"Başvuru Veri Kümeleri" seçeneğini belirleyin ve "+ Ekle" öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Merhaba zaman serisi Öngörüler başvuru veri kümesi - Ayrıntılar oluşturma](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="1c8bc-115">Merhaba hello başvuru veri kümesinin adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="1c8bc-116">Merhaba anahtar adını ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-116">Specify hello key name and its type.</span></span> <span data-ttu-id="1c8bc-117">Bu ada ve türe özelliğidir kullanılan toopick hello doğru olay kaynağınızda hello olaydan.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="1c8bc-118">Örneğin, "DeviceId" anahtar adı ve türü "Dize" olarak sağlarsanız, ardından zaman serisi türü "Dize" Merhaba gelen olay "DeviceID" Merhaba adında bir özellik giriş altyapısı arar Öngörüler hello.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="1c8bc-119">Birden fazla anahtar toojoin hello olayla sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="1c8bc-120">Merhaba özellik adı eşleşir büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-120">hello property name match is case-sensitive.</span></span>

     ![Merhaba zaman serisi Öngörüler başvuru veri kümesi - Ayrıntılar oluşturma](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="1c8bc-122">“Oluştur” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c8bc-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c8bc-123">Next steps</span></span>

* <span data-ttu-id="1c8bc-124">[Başvuru verilerini programlamayla yönetin](time-series-insights-manage-reference-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="1c8bc-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="1c8bc-125">Merhaba tam API başvuru için bkz: [başvuru veri API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) belge.</span><span class="sxs-lookup"><span data-stu-id="1c8bc-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
