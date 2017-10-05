---
title: "Azure Batch havuzu yeniden boyutlandırma complete olayını | Microsoft Docs"
description: "Batch havuzundaki başvurusunu complete olayını yeniden boyutlandırın."
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
ms.openlocfilehash: 7072293d98526812cb42ce9c2f8e33bfcafaa149
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="5760c-103">Havuzu yeniden boyutlandırma complete olayı</span><span class="sxs-lookup"><span data-stu-id="5760c-103">Pool resize complete event</span></span>

 <span data-ttu-id="5760c-104">Havuzu yeniden boyutlandırma tamamlandı veya başarısız olduğunda bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="5760c-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="5760c-105">Aşağıdaki örnek boyutu artar ve başarıyla tamamlandı bir havuz için havuzu yeniden boyutlandırma complete olayını gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="5760c-105">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "The operation succeeded"
}
```

|<span data-ttu-id="5760c-106">Öğesi</span><span class="sxs-lookup"><span data-stu-id="5760c-106">Element</span></span>|<span data-ttu-id="5760c-107">Tür</span><span class="sxs-lookup"><span data-stu-id="5760c-107">Type</span></span>|<span data-ttu-id="5760c-108">Notlar</span><span class="sxs-lookup"><span data-stu-id="5760c-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="5760c-109">id</span><span class="sxs-lookup"><span data-stu-id="5760c-109">id</span></span>|<span data-ttu-id="5760c-110">Dize</span><span class="sxs-lookup"><span data-stu-id="5760c-110">String</span></span>|<span data-ttu-id="5760c-111">Havuzun kimliği.</span><span class="sxs-lookup"><span data-stu-id="5760c-111">The id of the pool.</span></span>|
|<span data-ttu-id="5760c-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="5760c-112">nodeDeallocationOption</span></span>|<span data-ttu-id="5760c-113">Dize</span><span class="sxs-lookup"><span data-stu-id="5760c-113">String</span></span>|<span data-ttu-id="5760c-114">Havuz boyutunun küçülmesi durumunda ne zaman düğüm havuzdan kaldırılabilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="5760c-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="5760c-115">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5760c-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="5760c-116">**requeue** – yürütülen görevleri sonlandırır ve onları yeniden kuyruğa alır.</span><span class="sxs-lookup"><span data-stu-id="5760c-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="5760c-117">İş etkinleştirildiğinde görevler yeniden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5760c-117">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="5760c-118">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5760c-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="5760c-119">**sonlandırma** – çalışan görevlerin sonlandır.</span><span class="sxs-lookup"><span data-stu-id="5760c-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="5760c-120">Görevler yeniden çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="5760c-120">The tasks will not run again.</span></span> <span data-ttu-id="5760c-121">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5760c-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="5760c-122">**net_offline_option** – tamamlamak için izin şu anda çalışan görevler.</span><span class="sxs-lookup"><span data-stu-id="5760c-122">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="5760c-123">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="5760c-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="5760c-124">Tüm görevler tamamlandığında düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5760c-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="5760c-125">**Retaineddata** -izin şu anda çalışan görevlerin tamamlayın ve ardından tüm veri saklama sürelerini süresi dolmak üzere görev için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5760c-125">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="5760c-126">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="5760c-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="5760c-127">Tüm görev bekletme süreleri dolduğunda düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5760c-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="5760c-128">Requeue varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="5760c-128">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="5760c-129">Havuz boyutunun artırılması sonra değer kümesine **geçersiz**.</span><span class="sxs-lookup"><span data-stu-id="5760c-129">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="5760c-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="5760c-130">currentDedicated</span></span>|<span data-ttu-id="5760c-131">Int32</span><span class="sxs-lookup"><span data-stu-id="5760c-131">Int32</span></span>|<span data-ttu-id="5760c-132">Şu anda havuzuna atanmış işlem düğümleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="5760c-132">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="5760c-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="5760c-133">targetDedicated</span></span>|<span data-ttu-id="5760c-134">Int32</span><span class="sxs-lookup"><span data-stu-id="5760c-134">Int32</span></span>|<span data-ttu-id="5760c-135">Havuzu için istenen işlem düğümleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="5760c-135">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="5760c-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="5760c-136">enableAutoScale</span></span>|<span data-ttu-id="5760c-137">bool</span><span class="sxs-lookup"><span data-stu-id="5760c-137">Bool</span></span>|<span data-ttu-id="5760c-138">Havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5760c-138">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="5760c-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="5760c-139">isAutoPool</span></span>|<span data-ttu-id="5760c-140">bool</span><span class="sxs-lookup"><span data-stu-id="5760c-140">Bool</span></span>|<span data-ttu-id="5760c-141">Bir işin AutoPool mekanizması havuzu oluşturulup oluşturulmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5760c-141">Specifies whether the pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="5760c-142">startTime</span><span class="sxs-lookup"><span data-stu-id="5760c-142">startTime</span></span>|<span data-ttu-id="5760c-143">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="5760c-143">DateTime</span></span>|<span data-ttu-id="5760c-144">Havuzu yeniden boyutlandırma zaman başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="5760c-144">The time the pool resize started.</span></span>|
|<span data-ttu-id="5760c-145">EndTime</span><span class="sxs-lookup"><span data-stu-id="5760c-145">endTime</span></span>|<span data-ttu-id="5760c-146">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="5760c-146">DateTime</span></span>|<span data-ttu-id="5760c-147">Tamamlanan havuzu yeniden boyutlandırma süre.</span><span class="sxs-lookup"><span data-stu-id="5760c-147">The time the pool resize completed.</span></span>|
|<span data-ttu-id="5760c-148">ResultCode</span><span class="sxs-lookup"><span data-stu-id="5760c-148">resultCode</span></span>|<span data-ttu-id="5760c-149">Dize</span><span class="sxs-lookup"><span data-stu-id="5760c-149">String</span></span>|<span data-ttu-id="5760c-150">Yeniden boyutlandırma sonucu.</span><span class="sxs-lookup"><span data-stu-id="5760c-150">The result of the resize.</span></span>|
|<span data-ttu-id="5760c-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="5760c-151">resultMessage</span></span>|<span data-ttu-id="5760c-152">Dize</span><span class="sxs-lookup"><span data-stu-id="5760c-152">String</span></span>|<span data-ttu-id="5760c-153">Yeniden boyutlandırma hatası sonucu ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="5760c-153">The resize error includes the details of the result.</span></span><br /><br /> <span data-ttu-id="5760c-154">Yeniden boyutlandırma formu başarıyla tamamlanırsa işlemin başarılı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5760c-154">If the resize completed successfully it states that the operation succeeded.</span></span>|