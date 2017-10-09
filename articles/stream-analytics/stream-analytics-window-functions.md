---
title: "aaaIntroduction tooStream Analytics penceresi işlevleri | Microsoft Docs"
description: "Akış (dönen atlamalı, kayan) analizi hello üç pencere işlevleri hakkında bilgi edinin."
keywords: "dönen pencere, kayan pencere atlamalı pencere"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="cf7bf-104">Giriş tooStream Analytics penceresi işlevleri</span><span class="sxs-lookup"><span data-stu-id="cf7bf-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="cf7bf-105">Pek çok gerçek senaryoları akış, onu yalnızca zamana bağlı Windows'da bulunan hello verileri üzerinde gerekli tooperform işlemler saattir.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="cf7bf-106">Pencereleme işlevler için yerel destek karmaşık akış işleme işleri yazma, geliştirici üretkenliğine hello iğnenin taşır Azure akış analizi, anahtar bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="cf7bf-107">Akış analizi sağlar geliştiriciler toouse [ **dönen**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) ve [ **hareketli** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform zamana bağlı işlemleri veri akışı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="cf7bf-108">Değer belirtmeye olan tüm [penceresi](https://msdn.microsoft.com/library/dn835019.aspx) operations çıktı hello sonuçlarına **son** hello penceresinin.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="cf7bf-109">Merhaba penceresinde Hello çıktısını tek olay kullanılan hello üzerinde toplama işlevi tabanlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="cf7bf-110">Merhaba olay hello zaman damgası hello penceresinde hello ucunun sahip olur ve tüm pencere işlevleri sabit uzunluk ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="cf7bf-111">Son olarak tüm pencere işlevleri kullanılmalıdır önemli toonote olan bir [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Stream Analytics penceresi işlevleri kavramları](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="cf7bf-113">Atlayan pencere</span><span class="sxs-lookup"><span data-stu-id="cf7bf-113">Tumbling Window</span></span>
<span data-ttu-id="cf7bf-114">Dönen pencere işlevleri kullanılan toosegment ayrı zaman parçalara veri akışı olan ve bunları karşı işlevi Merhaba örneği aşağıdaki gibi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="cf7bf-115">Merhaba anahtar differentiators atlayan pencere, bunlar yinelemeniz, çakışmaması ve bir olay bir atlayan pencere daha toomore ait olamaz ' dir.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Giriş dönen stream Analytics penceresi işlevleri](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="cf7bf-117">Atlamalı pencere</span><span class="sxs-lookup"><span data-stu-id="cf7bf-117">Hopping Window</span></span>
<span data-ttu-id="cf7bf-118">Atlamalı pencere işlevleri atlama İleri zamanına göre sabit bir süre içinde.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="cf7bf-119">Olayları bir Hopping penceresi sonuç kümesi'den toomore ait olabilir. böylece bunların kolay toothink binebilir, dönen windows olarak olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="cf7bf-120">toomake Hopping penceresinde hello aynı biri yalnızca belirtirsiniz atlayan pencere hello atlama boyutu toobe hello aynı hello pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Stream Analytics penceresi atlamalı giriş işlevleri](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="cf7bf-122">Kayan pencere</span><span class="sxs-lookup"><span data-stu-id="cf7bf-122">Sliding Window</span></span>
<span data-ttu-id="cf7bf-123">Dönen veya atlamalı windows, farklı olarak, kayan pencere işlevleri bir çıktı üretir **yalnızca** olay oluştuğunda.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="cf7bf-124">Her penceresinde en az bir olay sahip olur ve hello penceresi sürekli bir € (epsilon) ileri taşır.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="cf7bf-125">Atlamalı Windows gibi olayların bir kayan pencere daha toomore ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Stream Analytics penceresi kayan giriş işlevleri](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="cf7bf-127">Pencere işlevleri ile ilgili Yardım alma</span><span class="sxs-lookup"><span data-stu-id="cf7bf-127">Getting help with Window functions</span></span>
<span data-ttu-id="cf7bf-128">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="cf7bf-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf7bf-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf7bf-129">Next steps</span></span>
* [<span data-ttu-id="cf7bf-130">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="cf7bf-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cf7bf-131">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="cf7bf-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cf7bf-132">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="cf7bf-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cf7bf-133">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="cf7bf-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cf7bf-134">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="cf7bf-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

