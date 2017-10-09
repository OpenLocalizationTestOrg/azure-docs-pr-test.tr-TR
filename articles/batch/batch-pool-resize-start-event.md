---
title: "aaa \"Azure Batch havuzu yeniden boyutlandır olayını Başlat | Microsoft Docs\""
description: "Batch havuzu yeniden boyutlandırma için başvuru olay başlatın."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="eea57-103">Havuzu yeniden boyutlandırma başlangıç olayı</span><span class="sxs-lookup"><span data-stu-id="eea57-103">Pool resize start event</span></span>

 <span data-ttu-id="eea57-104">Bir havuzu yeniden boyutlandırma başlatıldığında bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="eea57-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="eea57-105">Zaman uyumsuz bir olay Hello havuzu yeniden boyutlandırma olduğuna göre hello yeniden boyutlandırma sonra işlem yayılan bir havuzu yeniden boyutlandırma complete olayını toobe tamamlandıktan bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eea57-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="eea57-106">Aşağıdaki gösterildiği bir havuz 0 too2 düğümlerinden el ile yeniden boyutlandırma için havuzu yeniden boyutlandırma başlangıç olayı gövdesi hello örneğine hello yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="eea57-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="eea57-107">Öğesi</span><span class="sxs-lookup"><span data-stu-id="eea57-107">Element</span></span>|<span data-ttu-id="eea57-108">Tür</span><span class="sxs-lookup"><span data-stu-id="eea57-108">Type</span></span>|<span data-ttu-id="eea57-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="eea57-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="eea57-110">poolId</span><span class="sxs-lookup"><span data-stu-id="eea57-110">poolId</span></span>|<span data-ttu-id="eea57-111">Dize</span><span class="sxs-lookup"><span data-stu-id="eea57-111">String</span></span>|<span data-ttu-id="eea57-112">Merhaba havuzun Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="eea57-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="eea57-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="eea57-113">nodeDeallocationOption</span></span>|<span data-ttu-id="eea57-114">Dize</span><span class="sxs-lookup"><span data-stu-id="eea57-114">String</span></span>|<span data-ttu-id="eea57-115">Merhaba havuz boyutunun küçülmesi durumunda ne zaman düğümleri hello havuzdan kaldırılabilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="eea57-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="eea57-116">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="eea57-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="eea57-117">**requeue** – yürütülen görevleri sonlandırır ve onları yeniden kuyruğa alır.</span><span class="sxs-lookup"><span data-stu-id="eea57-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="eea57-118">Merhaba iş etkinleştirildiğinde hello görevler yeniden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="eea57-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="eea57-119">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="eea57-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="eea57-120">**sonlandırma** – çalışan görevlerin sonlandır.</span><span class="sxs-lookup"><span data-stu-id="eea57-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="eea57-121">Merhaba görevleri yeniden çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="eea57-121">hello tasks will not run again.</span></span> <span data-ttu-id="eea57-122">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="eea57-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="eea57-123">**net_offline_option** – çalışmakta olan görevleri toocomplete izin ver.</span><span class="sxs-lookup"><span data-stu-id="eea57-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="eea57-124">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="eea57-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="eea57-125">Tüm görevler tamamlandığında düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="eea57-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="eea57-126">**Retaineddata** - çalışmakta olan görevleri toocomplete izin verin ve sonra tüm veri bekletme dönemleri tooexpire görev için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="eea57-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="eea57-127">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="eea57-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="eea57-128">Tüm görev bekletme süreleri dolduğunda düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="eea57-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="eea57-129">requeue Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="eea57-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="eea57-130">Hello havuz boyutunun artırılması sonra hello değeri çok ayarlanır**geçersiz**.</span><span class="sxs-lookup"><span data-stu-id="eea57-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="eea57-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="eea57-131">currentDedicated</span></span>|<span data-ttu-id="eea57-132">Int32</span><span class="sxs-lookup"><span data-stu-id="eea57-132">Int32</span></span>|<span data-ttu-id="eea57-133">işlem düğümü sayısını Hello toohello havuzuna atanmış.</span><span class="sxs-lookup"><span data-stu-id="eea57-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="eea57-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="eea57-134">targetDedicated</span></span>|<span data-ttu-id="eea57-135">Int32</span><span class="sxs-lookup"><span data-stu-id="eea57-135">Int32</span></span>|<span data-ttu-id="eea57-136">Merhaba hello havuzu için istenen işlem düğümleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="eea57-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="eea57-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="eea57-137">enableAutoScale</span></span>|<span data-ttu-id="eea57-138">bool</span><span class="sxs-lookup"><span data-stu-id="eea57-138">Bool</span></span>|<span data-ttu-id="eea57-139">Merhaba havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="eea57-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="eea57-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="eea57-140">isAutoPool</span></span>|<span data-ttu-id="eea57-141">bool</span><span class="sxs-lookup"><span data-stu-id="eea57-141">Bool</span></span>|<span data-ttu-id="eea57-142">Speficies hello havuzu bir işin AutoPool mekanizması olup oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="eea57-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
