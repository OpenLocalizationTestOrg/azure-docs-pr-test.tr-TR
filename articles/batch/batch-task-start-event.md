---
title: "aaa \"Azure Batch görev başlangıç olayı | Microsoft Docs\""
description: "Toplu Görev Başlangıç olayı referansı."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="edc71-103">Görev Başlangıç olayı</span><span class="sxs-lookup"><span data-stu-id="edc71-103">Task start event</span></span>

 <span data-ttu-id="edc71-104">Bir görev bir işlem düğümünde zamanlanmış toostart silindikten sonra bu olay hello Zamanlayıcı tarafından yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="edc71-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="edc71-105">Merhaba görev denenen ya da yeniden kuyruğa bu olay yeniden hello aynı görevi, ancak hello yeniden deneme sayısı ve sistem görev sürümü buna göre güncelleştirilir yayınlaması olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="edc71-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="edc71-106">Merhaba aşağıdaki örnek bir görev başlangıç olayı hello gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="edc71-106">hello following example shows hello body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="edc71-107">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="edc71-107">Element name</span></span>|<span data-ttu-id="edc71-108">Tür</span><span class="sxs-lookup"><span data-stu-id="edc71-108">Type</span></span>|<span data-ttu-id="edc71-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="edc71-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="edc71-110">İş kimliği</span><span class="sxs-lookup"><span data-stu-id="edc71-110">jobId</span></span>|<span data-ttu-id="edc71-111">Dize</span><span class="sxs-lookup"><span data-stu-id="edc71-111">String</span></span>|<span data-ttu-id="edc71-112">Başlangıç görevini içeren hello işin Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="edc71-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="edc71-113">id</span><span class="sxs-lookup"><span data-stu-id="edc71-113">id</span></span>|<span data-ttu-id="edc71-114">Dize</span><span class="sxs-lookup"><span data-stu-id="edc71-114">String</span></span>|<span data-ttu-id="edc71-115">Merhaba görev Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="edc71-115">hello id of hello task.</span></span>|
|<span data-ttu-id="edc71-116">taskType</span><span class="sxs-lookup"><span data-stu-id="edc71-116">taskType</span></span>|<span data-ttu-id="edc71-117">Dize</span><span class="sxs-lookup"><span data-stu-id="edc71-117">String</span></span>|<span data-ttu-id="edc71-118">Başlangıç görevinin Hello türü.</span><span class="sxs-lookup"><span data-stu-id="edc71-118">hello type of hello task.</span></span> <span data-ttu-id="edc71-119">Bu, her bir iş yöneticisi görevi olduğunu gösteren'JobManager ' veya 'kullanıcı bir iş yöneticisi görevi değil belirten' olabilir.</span><span class="sxs-lookup"><span data-stu-id="edc71-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="edc71-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="edc71-120">systemTaskVersion</span></span>|<span data-ttu-id="edc71-121">Int32</span><span class="sxs-lookup"><span data-stu-id="edc71-121">Int32</span></span>|<span data-ttu-id="edc71-122">Bir görev hello iç yeniden deneme sayacı budur.</span><span class="sxs-lookup"><span data-stu-id="edc71-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="edc71-123">Dahili olarak hello toplu işlem hizmeti görevi tooaccount geçici sorunlar için yeniden deneyebilir.</span><span class="sxs-lookup"><span data-stu-id="edc71-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="edc71-124">Bu sorunları işlem düğümlerinden iç zamanlama hataları veya deneme toorecover hatalı bir duruma içerebilir.</span><span class="sxs-lookup"><span data-stu-id="edc71-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="edc71-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="edc71-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="edc71-126">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="edc71-126">Complex Type</span></span>|<span data-ttu-id="edc71-127">Merhaba işlem düğümü üzerinde hangi hello görevi çalıştı hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="edc71-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="edc71-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="edc71-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="edc71-129">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="edc71-129">Complex Type</span></span>|<span data-ttu-id="edc71-130">Çok örnekli görev birden çok işlem düğümleri gerektiren hello görev olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="edc71-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="edc71-131">Bkz: [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="edc71-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="edc71-132">kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="edc71-132">constraints</span></span>](#constraints)|<span data-ttu-id="edc71-133">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="edc71-133">Complex Type</span></span>|<span data-ttu-id="edc71-134">toothis görev uygulamak hello yürütme kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="edc71-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="edc71-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="edc71-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="edc71-136">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="edc71-136">Complex Type</span></span>|<span data-ttu-id="edc71-137">Başlangıç görevi hello yürütme hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="edc71-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="edc71-138"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="edc71-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="edc71-139">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="edc71-139">Element name</span></span>|<span data-ttu-id="edc71-140">Tür</span><span class="sxs-lookup"><span data-stu-id="edc71-140">Type</span></span>|<span data-ttu-id="edc71-141">Notlar</span><span class="sxs-lookup"><span data-stu-id="edc71-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="edc71-142">poolId</span><span class="sxs-lookup"><span data-stu-id="edc71-142">poolId</span></span>|<span data-ttu-id="edc71-143">Dize</span><span class="sxs-lookup"><span data-stu-id="edc71-143">String</span></span>|<span data-ttu-id="edc71-144">Görev hangi hello çalıştı hello havuzun Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="edc71-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="edc71-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="edc71-145">nodeId</span></span>|<span data-ttu-id="edc71-146">Dize</span><span class="sxs-lookup"><span data-stu-id="edc71-146">String</span></span>|<span data-ttu-id="edc71-147">Görev hangi hello çalıştı hello düğümün Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="edc71-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="edc71-148"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="edc71-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="edc71-149">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="edc71-149">Element name</span></span>|<span data-ttu-id="edc71-150">Tür</span><span class="sxs-lookup"><span data-stu-id="edc71-150">Type</span></span>|<span data-ttu-id="edc71-151">Notlar</span><span class="sxs-lookup"><span data-stu-id="edc71-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="edc71-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="edc71-152">numberOfInstances</span></span>|<span data-ttu-id="edc71-153">Int</span><span class="sxs-lookup"><span data-stu-id="edc71-153">Int</span></span>|<span data-ttu-id="edc71-154">işlem düğümü başlangıç görevi tarafından istenen Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="edc71-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="edc71-155"><a name="constraints"></a>kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="edc71-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="edc71-156">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="edc71-156">Element name</span></span>|<span data-ttu-id="edc71-157">Tür</span><span class="sxs-lookup"><span data-stu-id="edc71-157">Type</span></span>|<span data-ttu-id="edc71-158">Notlar</span><span class="sxs-lookup"><span data-stu-id="edc71-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="edc71-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="edc71-159">maxTaskRetryCount</span></span>|<span data-ttu-id="edc71-160">Int32</span><span class="sxs-lookup"><span data-stu-id="edc71-160">Int32</span></span>|<span data-ttu-id="edc71-161">en fazla kaç kez hello görev denenen hello.</span><span class="sxs-lookup"><span data-stu-id="edc71-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="edc71-162">çıkış kodu sıfır değilse hello toplu işlem hizmeti görevi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="edc71-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="edc71-163">Bu değer özellikle hello yeniden deneme sayısı kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="edc71-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="edc71-164">Merhaba Batch hizmeti hello görev bir kez dener ve ardından toothis yeniden deneme sınırı.</span><span class="sxs-lookup"><span data-stu-id="edc71-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="edc71-165">Örneğin, Hello en fazla yeniden deneme sayısı 3 ise, toplu bir görev too4 (bir ilk deneyin ve 3 yeniden denemeyi) kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="edc71-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="edc71-166">Merhaba maksimum yeniden deneme sayısının 0 olması durumunda hello toplu işlem hizmetinin görevleri yeniden denemez.</span><span class="sxs-lookup"><span data-stu-id="edc71-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="edc71-167">Merhaba en fazla yeniden deneme sayısı -1 ise, hello Batch hizmetinin görevleri sınır olmaksızın yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="edc71-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="edc71-168">0 (yeniden deneme) Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="edc71-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="edc71-169"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="edc71-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="edc71-170">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="edc71-170">Element name</span></span>|<span data-ttu-id="edc71-171">Tür</span><span class="sxs-lookup"><span data-stu-id="edc71-171">Type</span></span>|<span data-ttu-id="edc71-172">Notlar</span><span class="sxs-lookup"><span data-stu-id="edc71-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="edc71-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="edc71-173">retryCount</span></span>|<span data-ttu-id="edc71-174">Int32</span><span class="sxs-lookup"><span data-stu-id="edc71-174">Int32</span></span>|<span data-ttu-id="edc71-175">Merhaba görev hello Batch hizmeti tarafından denenen sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="edc71-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="edc71-176">toohello MaxTaskRetryCount belirtilen sıfır olmayan çıkış kodu ile bulunup bulunmadığını hello görev denenir</span><span class="sxs-lookup"><span data-stu-id="edc71-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
