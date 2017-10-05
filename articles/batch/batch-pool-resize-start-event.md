---
title: "Azure Batch havuzu yeniden boyutlandır olayını Başlat | Microsoft Docs"
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
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="52e3c-103">Havuzu yeniden boyutlandırma başlangıç olayı</span><span class="sxs-lookup"><span data-stu-id="52e3c-103">Pool resize start event</span></span>

 <span data-ttu-id="52e3c-104">Bir havuzu yeniden boyutlandırma başlatıldığında bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="52e3c-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="52e3c-105">Zaman uyumsuz bir olay havuzu yeniden boyutlandırma olduğuna göre yeniden boyutlandırma işlemi tamamlandıktan sonra yayınlaması için havuzu yeniden boyutlandırma complete olayını bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52e3c-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="52e3c-106">Aşağıdaki örnek, bir havuz 0'dan 2 düğümlerine el ile bir yeniden boyutlandırma ile yeniden boyutlandırma için havuzu yeniden boyutlandırma başlangıç olayı gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="52e3c-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="52e3c-107">Öğesi</span><span class="sxs-lookup"><span data-stu-id="52e3c-107">Element</span></span>|<span data-ttu-id="52e3c-108">Tür</span><span class="sxs-lookup"><span data-stu-id="52e3c-108">Type</span></span>|<span data-ttu-id="52e3c-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="52e3c-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="52e3c-110">poolId</span><span class="sxs-lookup"><span data-stu-id="52e3c-110">poolId</span></span>|<span data-ttu-id="52e3c-111">Dize</span><span class="sxs-lookup"><span data-stu-id="52e3c-111">String</span></span>|<span data-ttu-id="52e3c-112">Havuzun kimliği.</span><span class="sxs-lookup"><span data-stu-id="52e3c-112">The id of the pool.</span></span>|
|<span data-ttu-id="52e3c-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="52e3c-113">nodeDeallocationOption</span></span>|<span data-ttu-id="52e3c-114">Dize</span><span class="sxs-lookup"><span data-stu-id="52e3c-114">String</span></span>|<span data-ttu-id="52e3c-115">Havuz boyutunun küçülmesi durumunda ne zaman düğüm havuzdan kaldırılabilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="52e3c-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="52e3c-116">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="52e3c-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="52e3c-117">**requeue** – yürütülen görevleri sonlandırır ve onları yeniden kuyruğa alır.</span><span class="sxs-lookup"><span data-stu-id="52e3c-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="52e3c-118">İş etkinleştirildiğinde görevler yeniden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="52e3c-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="52e3c-119">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="52e3c-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="52e3c-120">**sonlandırma** – çalışan görevlerin sonlandır.</span><span class="sxs-lookup"><span data-stu-id="52e3c-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="52e3c-121">Görevler yeniden çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="52e3c-121">The tasks will not run again.</span></span> <span data-ttu-id="52e3c-122">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="52e3c-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="52e3c-123">**net_offline_option** – tamamlamak için izin şu anda çalışan görevler.</span><span class="sxs-lookup"><span data-stu-id="52e3c-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="52e3c-124">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="52e3c-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="52e3c-125">Tüm görevler tamamlandığında düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="52e3c-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="52e3c-126">**Retaineddata** -izin şu anda çalışan görevlerin tamamlayın ve ardından tüm veri saklama sürelerini süresi dolmak üzere görev için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="52e3c-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="52e3c-127">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="52e3c-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="52e3c-128">Tüm görev bekletme süreleri dolduğunda düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="52e3c-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="52e3c-129">Requeue varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="52e3c-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="52e3c-130">Havuz boyutunun artırılması sonra değer kümesine **geçersiz**.</span><span class="sxs-lookup"><span data-stu-id="52e3c-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="52e3c-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="52e3c-131">currentDedicated</span></span>|<span data-ttu-id="52e3c-132">Int32</span><span class="sxs-lookup"><span data-stu-id="52e3c-132">Int32</span></span>|<span data-ttu-id="52e3c-133">Şu anda havuzuna atanmış işlem düğümleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="52e3c-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="52e3c-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="52e3c-134">targetDedicated</span></span>|<span data-ttu-id="52e3c-135">Int32</span><span class="sxs-lookup"><span data-stu-id="52e3c-135">Int32</span></span>|<span data-ttu-id="52e3c-136">Havuzu için istenen işlem düğümleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="52e3c-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="52e3c-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="52e3c-137">enableAutoScale</span></span>|<span data-ttu-id="52e3c-138">bool</span><span class="sxs-lookup"><span data-stu-id="52e3c-138">Bool</span></span>|<span data-ttu-id="52e3c-139">Havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="52e3c-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="52e3c-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="52e3c-140">isAutoPool</span></span>|<span data-ttu-id="52e3c-141">bool</span><span class="sxs-lookup"><span data-stu-id="52e3c-141">Bool</span></span>|<span data-ttu-id="52e3c-142">Speficies havuzu bir işin AutoPool mekanizması olup oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="52e3c-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
