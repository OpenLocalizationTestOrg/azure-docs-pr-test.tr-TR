---
title: "aaa \"Azure Batch havuzu yeniden boyutlandırma complete olayını | Microsoft Docs\""
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="9c566-103">Havuzu yeniden boyutlandırma complete olayı</span><span class="sxs-lookup"><span data-stu-id="9c566-103">Pool resize complete event</span></span>

 <span data-ttu-id="9c566-104">Havuzu yeniden boyutlandırma tamamlandı veya başarısız olduğunda bu olay yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="9c566-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="9c566-105">Merhaba aşağıdaki örnek boyutu artar ve başarıyla tamamlandı bir havuz için havuzu yeniden boyutlandırma complete olayını hello gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c566-105">hello following example shows hello body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

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
    "resizeError": "hello operation succeeded"
}
```

|<span data-ttu-id="9c566-106">Öğesi</span><span class="sxs-lookup"><span data-stu-id="9c566-106">Element</span></span>|<span data-ttu-id="9c566-107">Tür</span><span class="sxs-lookup"><span data-stu-id="9c566-107">Type</span></span>|<span data-ttu-id="9c566-108">Notlar</span><span class="sxs-lookup"><span data-stu-id="9c566-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="9c566-109">id</span><span class="sxs-lookup"><span data-stu-id="9c566-109">id</span></span>|<span data-ttu-id="9c566-110">Dize</span><span class="sxs-lookup"><span data-stu-id="9c566-110">String</span></span>|<span data-ttu-id="9c566-111">Merhaba havuzun Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="9c566-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="9c566-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="9c566-112">nodeDeallocationOption</span></span>|<span data-ttu-id="9c566-113">Dize</span><span class="sxs-lookup"><span data-stu-id="9c566-113">String</span></span>|<span data-ttu-id="9c566-114">Merhaba havuz boyutunun küçülmesi durumunda ne zaman düğümleri hello havuzdan kaldırılabilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="9c566-114">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="9c566-115">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9c566-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="9c566-116">**requeue** – yürütülen görevleri sonlandırır ve onları yeniden kuyruğa alır.</span><span class="sxs-lookup"><span data-stu-id="9c566-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="9c566-117">Merhaba iş etkinleştirildiğinde hello görevler yeniden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9c566-117">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="9c566-118">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9c566-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="9c566-119">**sonlandırma** – çalışan görevlerin sonlandır.</span><span class="sxs-lookup"><span data-stu-id="9c566-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="9c566-120">Merhaba görevleri yeniden çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9c566-120">hello tasks will not run again.</span></span> <span data-ttu-id="9c566-121">Görevler sonlandırıldı hemen düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9c566-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="9c566-122">**net_offline_option** – çalışmakta olan görevleri toocomplete izin ver.</span><span class="sxs-lookup"><span data-stu-id="9c566-122">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="9c566-123">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="9c566-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="9c566-124">Tüm görevler tamamlandığında düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9c566-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="9c566-125">**Retaineddata** - çalışmakta olan görevleri toocomplete izin verin ve sonra tüm veri bekletme dönemleri tooexpire görev için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c566-125">**Retaineddata** -  Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="9c566-126">Beklenirken hiç yeni görev zamanlamaz.</span><span class="sxs-lookup"><span data-stu-id="9c566-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="9c566-127">Tüm görev bekletme süreleri dolduğunda düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9c566-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="9c566-128">requeue Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="9c566-128">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="9c566-129">Hello havuz boyutunun artırılması sonra hello değeri çok ayarlanır**geçersiz**.</span><span class="sxs-lookup"><span data-stu-id="9c566-129">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="9c566-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="9c566-130">currentDedicated</span></span>|<span data-ttu-id="9c566-131">Int32</span><span class="sxs-lookup"><span data-stu-id="9c566-131">Int32</span></span>|<span data-ttu-id="9c566-132">işlem düğümü sayısını Hello toohello havuzuna atanmış.</span><span class="sxs-lookup"><span data-stu-id="9c566-132">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="9c566-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="9c566-133">targetDedicated</span></span>|<span data-ttu-id="9c566-134">Int32</span><span class="sxs-lookup"><span data-stu-id="9c566-134">Int32</span></span>|<span data-ttu-id="9c566-135">Merhaba hello havuzu için istenen işlem düğümleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="9c566-135">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="9c566-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="9c566-136">enableAutoScale</span></span>|<span data-ttu-id="9c566-137">bool</span><span class="sxs-lookup"><span data-stu-id="9c566-137">Bool</span></span>|<span data-ttu-id="9c566-138">Merhaba havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9c566-138">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="9c566-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="9c566-139">isAutoPool</span></span>|<span data-ttu-id="9c566-140">bool</span><span class="sxs-lookup"><span data-stu-id="9c566-140">Bool</span></span>|<span data-ttu-id="9c566-141">Bir işin AutoPool mekanizması Hello havuzu oluşturulup oluşturulmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9c566-141">Specifies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="9c566-142">startTime</span><span class="sxs-lookup"><span data-stu-id="9c566-142">startTime</span></span>|<span data-ttu-id="9c566-143">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="9c566-143">DateTime</span></span>|<span data-ttu-id="9c566-144">Merhaba havuzu yeniden boyutlandırma hello zaman başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9c566-144">hello time hello pool resize started.</span></span>|
|<span data-ttu-id="9c566-145">endTime</span><span class="sxs-lookup"><span data-stu-id="9c566-145">endTime</span></span>|<span data-ttu-id="9c566-146">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="9c566-146">DateTime</span></span>|<span data-ttu-id="9c566-147">Merhaba hello havuzu yeniden boyutlandırma süresi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="9c566-147">hello time hello pool resize completed.</span></span>|
|<span data-ttu-id="9c566-148">ResultCode</span><span class="sxs-lookup"><span data-stu-id="9c566-148">resultCode</span></span>|<span data-ttu-id="9c566-149">Dize</span><span class="sxs-lookup"><span data-stu-id="9c566-149">String</span></span>|<span data-ttu-id="9c566-150">Merhaba Hello sonucunu yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="9c566-150">hello result of hello resize.</span></span>|
|<span data-ttu-id="9c566-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="9c566-151">resultMessage</span></span>|<span data-ttu-id="9c566-152">Dize</span><span class="sxs-lookup"><span data-stu-id="9c566-152">String</span></span>|<span data-ttu-id="9c566-153">Merhaba yeniden boyutlandırma hatası hello sonuç hello ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9c566-153">hello resize error includes hello details of hello result.</span></span><br /><br /> <span data-ttu-id="9c566-154">Başarıyla Hello yeniden boyutlandırmak, işlemi başarılı oldu hello durumları tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="9c566-154">If hello resize completed successfully it states that hello operation succeeded.</span></span>|
