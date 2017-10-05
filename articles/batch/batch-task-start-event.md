---
title: "Azure Batch görev başlangıç olayı | Microsoft Docs"
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="b6dc0-103">Görev Başlangıç olayı</span><span class="sxs-lookup"><span data-stu-id="b6dc0-103">Task start event</span></span>

 <span data-ttu-id="b6dc0-104">Bu olay, bir görev bir işlem düğümünde başlatmak için Zamanlayıcı tarafından zamanlandı sonra yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="b6dc0-105">Görev yeniden deneme işlemi ya da yeniden kuyruğa bu olay yeniden aynı görevi, ancak yeniden deneme sayısı için yayınlaması ve sistem görev sürümü buna göre güncelleştirilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="b6dc0-106">Aşağıdaki örnek, bir görevin Başlat olay gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-106">The following example shows the body of a task start event.</span></span>

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

|<span data-ttu-id="b6dc0-107">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b6dc0-107">Element name</span></span>|<span data-ttu-id="b6dc0-108">Tür</span><span class="sxs-lookup"><span data-stu-id="b6dc0-108">Type</span></span>|<span data-ttu-id="b6dc0-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="b6dc0-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b6dc0-110">İş kimliği</span><span class="sxs-lookup"><span data-stu-id="b6dc0-110">jobId</span></span>|<span data-ttu-id="b6dc0-111">Dize</span><span class="sxs-lookup"><span data-stu-id="b6dc0-111">String</span></span>|<span data-ttu-id="b6dc0-112">Görevi içeren işi kimliği.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="b6dc0-113">id</span><span class="sxs-lookup"><span data-stu-id="b6dc0-113">id</span></span>|<span data-ttu-id="b6dc0-114">Dize</span><span class="sxs-lookup"><span data-stu-id="b6dc0-114">String</span></span>|<span data-ttu-id="b6dc0-115">Görev kimliği.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-115">The id of the task.</span></span>|
|<span data-ttu-id="b6dc0-116">taskType</span><span class="sxs-lookup"><span data-stu-id="b6dc0-116">taskType</span></span>|<span data-ttu-id="b6dc0-117">Dize</span><span class="sxs-lookup"><span data-stu-id="b6dc0-117">String</span></span>|<span data-ttu-id="b6dc0-118">Görev türü.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-118">The type of the task.</span></span> <span data-ttu-id="b6dc0-119">Bu, her bir iş yöneticisi görevi olduğunu gösteren'JobManager ' veya 'kullanıcı bir iş yöneticisi görevi değil belirten' olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="b6dc0-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="b6dc0-120">systemTaskVersion</span></span>|<span data-ttu-id="b6dc0-121">Int32</span><span class="sxs-lookup"><span data-stu-id="b6dc0-121">Int32</span></span>|<span data-ttu-id="b6dc0-122">Bir görev iç yeniden deneme sayacı budur.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="b6dc0-123">Dahili olarak Batch hizmeti geçici sorunlar için hesap için bir görevi yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="b6dc0-124">Bu sorunları iç zamanlama hatalar içerebilir veya kurtarma girişimleri işlem düğümleri hatalı bir durumda.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="b6dc0-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="b6dc0-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="b6dc0-126">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="b6dc0-126">Complex Type</span></span>|<span data-ttu-id="b6dc0-127">İşlem düğümünde görevin çalıştırıldığı hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="b6dc0-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="b6dc0-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="b6dc0-129">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="b6dc0-129">Complex Type</span></span>|<span data-ttu-id="b6dc0-130">Görevi birden çok işlem düğümleri gerektiren çok örnekli görev olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="b6dc0-131">Bkz: [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="b6dc0-132">kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="b6dc0-132">constraints</span></span>](#constraints)|<span data-ttu-id="b6dc0-133">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="b6dc0-133">Complex Type</span></span>|<span data-ttu-id="b6dc0-134">Bu görev için geçerli yürütme kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="b6dc0-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="b6dc0-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="b6dc0-136">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="b6dc0-136">Complex Type</span></span>|<span data-ttu-id="b6dc0-137">Görevin yürütülmesi hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="b6dc0-138"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="b6dc0-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="b6dc0-139">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b6dc0-139">Element name</span></span>|<span data-ttu-id="b6dc0-140">Tür</span><span class="sxs-lookup"><span data-stu-id="b6dc0-140">Type</span></span>|<span data-ttu-id="b6dc0-141">Notlar</span><span class="sxs-lookup"><span data-stu-id="b6dc0-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b6dc0-142">poolId</span><span class="sxs-lookup"><span data-stu-id="b6dc0-142">poolId</span></span>|<span data-ttu-id="b6dc0-143">Dize</span><span class="sxs-lookup"><span data-stu-id="b6dc0-143">String</span></span>|<span data-ttu-id="b6dc0-144">Görevin çalıştırıldığı havuzun kimliği.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="b6dc0-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="b6dc0-145">nodeId</span></span>|<span data-ttu-id="b6dc0-146">Dize</span><span class="sxs-lookup"><span data-stu-id="b6dc0-146">String</span></span>|<span data-ttu-id="b6dc0-147">Görevin çalıştırıldığı düğümün kimliği.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="b6dc0-148"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="b6dc0-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="b6dc0-149">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b6dc0-149">Element name</span></span>|<span data-ttu-id="b6dc0-150">Tür</span><span class="sxs-lookup"><span data-stu-id="b6dc0-150">Type</span></span>|<span data-ttu-id="b6dc0-151">Notlar</span><span class="sxs-lookup"><span data-stu-id="b6dc0-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b6dc0-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="b6dc0-152">numberOfInstances</span></span>|<span data-ttu-id="b6dc0-153">Int</span><span class="sxs-lookup"><span data-stu-id="b6dc0-153">Int</span></span>|<span data-ttu-id="b6dc0-154">Görevin gerektirdiği işlem düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="b6dc0-155"><a name="constraints"></a>kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="b6dc0-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="b6dc0-156">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b6dc0-156">Element name</span></span>|<span data-ttu-id="b6dc0-157">Tür</span><span class="sxs-lookup"><span data-stu-id="b6dc0-157">Type</span></span>|<span data-ttu-id="b6dc0-158">Notlar</span><span class="sxs-lookup"><span data-stu-id="b6dc0-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b6dc0-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="b6dc0-159">maxTaskRetryCount</span></span>|<span data-ttu-id="b6dc0-160">Int32</span><span class="sxs-lookup"><span data-stu-id="b6dc0-160">Int32</span></span>|<span data-ttu-id="b6dc0-161">Maksimum görev yeniden sayısı.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="b6dc0-162">Çıkış kodu sıfır değilse toplu işlem hizmeti görevi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="b6dc0-163">Bu değer özellikle yeniden deneme sayısını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="b6dc0-164">Toplu işlem hizmeti görevi bir kez dener ve bu sınıra kadar daha sonra yeniden deneyebilir.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="b6dc0-165">Örneğin, en fazla yeniden deneme sayısı 3, toplu çalıştığında bir görevin en fazla ise 4 (bir ilk deneyin ve 3 yeniden denemeyi) zaman.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="b6dc0-166">En fazla yeniden deneme sayısının 0 olması durumunda toplu işlem hizmetinin görevleri yeniden denemez.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="b6dc0-167">En fazla yeniden deneme sayısı -1 ise, Batch hizmeti görevleri sınır olmaksızın yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="b6dc0-168">Varsayılan değer 0 (yeniden deneme)'dır.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="b6dc0-169"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="b6dc0-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="b6dc0-170">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b6dc0-170">Element name</span></span>|<span data-ttu-id="b6dc0-171">Tür</span><span class="sxs-lookup"><span data-stu-id="b6dc0-171">Type</span></span>|<span data-ttu-id="b6dc0-172">Notlar</span><span class="sxs-lookup"><span data-stu-id="b6dc0-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b6dc0-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="b6dc0-173">retryCount</span></span>|<span data-ttu-id="b6dc0-174">Int32</span><span class="sxs-lookup"><span data-stu-id="b6dc0-174">Int32</span></span>|<span data-ttu-id="b6dc0-175">Görev Batch hizmeti tarafından denenen sayısı.</span><span class="sxs-lookup"><span data-stu-id="b6dc0-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="b6dc0-176">Belirtilen MaxTaskRetryCount kadar bir sıfır olmayan çıkış kodu ile bulunup bulunmadığını görev denenir</span><span class="sxs-lookup"><span data-stu-id="b6dc0-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
