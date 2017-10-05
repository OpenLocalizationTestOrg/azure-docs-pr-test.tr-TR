---
title: "Azure Batch görev complete olayını | Microsoft Docs"
description: "Toplu Görev complete olayını referansı."
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
ms.openlocfilehash: 015adf7dbc47c29a78df4e4889b2ee1ddcccdd8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="task-complete-event"></a><span data-ttu-id="d3fcd-103">Görev tamamlandı olayı</span><span class="sxs-lookup"><span data-stu-id="d3fcd-103">Task complete event</span></span>

 <span data-ttu-id="d3fcd-104">Bu olay, bir görev tamamlandığında, çıkış kodu bağımsız olarak yayılır.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-104">This event is emitted once a task is completed, regardless of the exit code.</span></span> <span data-ttu-id="d3fcd-105">Bu olay, bir görevin süresini görevi çalıştı ve bu denenen olup olmadığını belirlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-105">This event can be used to determine the duration of a task, where the task ran, and whether it was retried.</span></span>


 <span data-ttu-id="d3fcd-106">Aşağıdaki örnek, bir görev complete olayını gövdesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-106">The following example shows the body of a task complete event.</span></span>

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
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="d3fcd-107">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="d3fcd-107">Element name</span></span>|<span data-ttu-id="d3fcd-108">Tür</span><span class="sxs-lookup"><span data-stu-id="d3fcd-108">Type</span></span>|<span data-ttu-id="d3fcd-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="d3fcd-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d3fcd-110">İş kimliği</span><span class="sxs-lookup"><span data-stu-id="d3fcd-110">jobId</span></span>|<span data-ttu-id="d3fcd-111">Dize</span><span class="sxs-lookup"><span data-stu-id="d3fcd-111">String</span></span>|<span data-ttu-id="d3fcd-112">Görevi içeren işi kimliği.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="d3fcd-113">id</span><span class="sxs-lookup"><span data-stu-id="d3fcd-113">id</span></span>|<span data-ttu-id="d3fcd-114">Dize</span><span class="sxs-lookup"><span data-stu-id="d3fcd-114">String</span></span>|<span data-ttu-id="d3fcd-115">Görev kimliği.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-115">The id of the task.</span></span>|
|<span data-ttu-id="d3fcd-116">taskType</span><span class="sxs-lookup"><span data-stu-id="d3fcd-116">taskType</span></span>|<span data-ttu-id="d3fcd-117">Dize</span><span class="sxs-lookup"><span data-stu-id="d3fcd-117">String</span></span>|<span data-ttu-id="d3fcd-118">Görev türü.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-118">The type of the task.</span></span> <span data-ttu-id="d3fcd-119">Bu, her bir iş yöneticisi görevi olduğunu gösteren'JobManager ' veya 'kullanıcı bir iş yöneticisi görevi değil belirten' olabilir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="d3fcd-120">Bu olay, iş hazırlama görevleri, iş sürüm görevleri veya başlangıç görevleri için gösterilen değil.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="d3fcd-121">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="d3fcd-121">systemTaskVersion</span></span>|<span data-ttu-id="d3fcd-122">Int32</span><span class="sxs-lookup"><span data-stu-id="d3fcd-122">Int32</span></span>|<span data-ttu-id="d3fcd-123">Bir görev iç yeniden deneme sayacı budur.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-123">This is the internal retry counter on a task.</span></span> <span data-ttu-id="d3fcd-124">Dahili olarak Batch hizmeti geçici sorunlar için hesap için bir görevi yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-124">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="d3fcd-125">Bu sorunları iç zamanlama hatalar içerebilir veya kurtarma girişimleri işlem düğümleri hatalı bir durumda.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-125">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="d3fcd-126">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d3fcd-126">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="d3fcd-127">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="d3fcd-127">Complex Type</span></span>|<span data-ttu-id="d3fcd-128">İşlem düğümünde görevin çalıştırıldığı hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-128">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="d3fcd-129">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d3fcd-129">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="d3fcd-130">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="d3fcd-130">Complex Type</span></span>|<span data-ttu-id="d3fcd-131">Görevi birden çok işlem düğümleri gerektiren çok örnekli görev olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-131">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="d3fcd-132">Bkz: [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="d3fcd-133">kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="d3fcd-133">constraints</span></span>](#constraints)|<span data-ttu-id="d3fcd-134">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="d3fcd-134">Complex Type</span></span>|<span data-ttu-id="d3fcd-135">Bu görev için geçerli yürütme kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-135">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="d3fcd-136">executionInfo</span><span class="sxs-lookup"><span data-stu-id="d3fcd-136">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="d3fcd-137">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="d3fcd-137">Complex Type</span></span>|<span data-ttu-id="d3fcd-138">Görevin yürütülmesi hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-138">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="d3fcd-139"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d3fcd-139"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="d3fcd-140">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="d3fcd-140">Element name</span></span>|<span data-ttu-id="d3fcd-141">Tür</span><span class="sxs-lookup"><span data-stu-id="d3fcd-141">Type</span></span>|<span data-ttu-id="d3fcd-142">Notlar</span><span class="sxs-lookup"><span data-stu-id="d3fcd-142">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d3fcd-143">poolId</span><span class="sxs-lookup"><span data-stu-id="d3fcd-143">poolId</span></span>|<span data-ttu-id="d3fcd-144">Dize</span><span class="sxs-lookup"><span data-stu-id="d3fcd-144">String</span></span>|<span data-ttu-id="d3fcd-145">Görevin çalıştırıldığı havuzun kimliği.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-145">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="d3fcd-146">nodeId</span><span class="sxs-lookup"><span data-stu-id="d3fcd-146">nodeId</span></span>|<span data-ttu-id="d3fcd-147">Dize</span><span class="sxs-lookup"><span data-stu-id="d3fcd-147">String</span></span>|<span data-ttu-id="d3fcd-148">Görevin çalıştırıldığı düğümün kimliği.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-148">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="d3fcd-149"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d3fcd-149"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="d3fcd-150">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="d3fcd-150">Element name</span></span>|<span data-ttu-id="d3fcd-151">Tür</span><span class="sxs-lookup"><span data-stu-id="d3fcd-151">Type</span></span>|<span data-ttu-id="d3fcd-152">Notlar</span><span class="sxs-lookup"><span data-stu-id="d3fcd-152">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d3fcd-153">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="d3fcd-153">numberOfInstances</span></span>|<span data-ttu-id="d3fcd-154">Int32</span><span class="sxs-lookup"><span data-stu-id="d3fcd-154">Int32</span></span>|<span data-ttu-id="d3fcd-155">Görevin gerektirdiği işlem düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-155">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="d3fcd-156"><a name="constraints"></a>kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="d3fcd-156"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="d3fcd-157">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="d3fcd-157">Element name</span></span>|<span data-ttu-id="d3fcd-158">Tür</span><span class="sxs-lookup"><span data-stu-id="d3fcd-158">Type</span></span>|<span data-ttu-id="d3fcd-159">Notlar</span><span class="sxs-lookup"><span data-stu-id="d3fcd-159">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d3fcd-160">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="d3fcd-160">maxTaskRetryCount</span></span>|<span data-ttu-id="d3fcd-161">Int32</span><span class="sxs-lookup"><span data-stu-id="d3fcd-161">Int32</span></span>|<span data-ttu-id="d3fcd-162">Maksimum görev yeniden sayısı.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-162">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="d3fcd-163">Çıkış kodu sıfır değilse toplu işlem hizmeti görevi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-163">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="d3fcd-164">Bu değer özellikle yeniden deneme sayısını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-164">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="d3fcd-165">Toplu işlem hizmeti görevi bir kez dener ve bu sınıra kadar daha sonra yeniden deneyebilir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-165">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="d3fcd-166">Örneğin, en fazla yeniden deneme sayısı 3, toplu çalıştığında bir görevin en fazla ise 4 (bir ilk deneyin ve 3 yeniden denemeyi) zaman.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-166">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="d3fcd-167">En fazla yeniden deneme sayısının 0 olması durumunda toplu işlem hizmetinin görevleri yeniden denemez.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-167">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="d3fcd-168">En fazla yeniden deneme sayısı -1 ise, Batch hizmeti görevleri sınır olmaksızın yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-168">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="d3fcd-169">Varsayılan değer 0 (yeniden deneme)'dır.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-169">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="d3fcd-170"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="d3fcd-170"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="d3fcd-171">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="d3fcd-171">Element name</span></span>|<span data-ttu-id="d3fcd-172">Tür</span><span class="sxs-lookup"><span data-stu-id="d3fcd-172">Type</span></span>|<span data-ttu-id="d3fcd-173">Notlar</span><span class="sxs-lookup"><span data-stu-id="d3fcd-173">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d3fcd-174">startTime</span><span class="sxs-lookup"><span data-stu-id="d3fcd-174">startTime</span></span>|<span data-ttu-id="d3fcd-175">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d3fcd-175">DateTime</span></span>|<span data-ttu-id="d3fcd-176">Görev çalıştıran başladığı zaman.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-176">The time at which the task started running.</span></span> <span data-ttu-id="d3fcd-177">'Çalışıyor' karşılık gelen **çalıştıran** görev kaynak dosyaları veya uygulama paketleri belirtiyorsa, başlangıç saati görev başladığı indirilirken veya bunlar dağıtma zaman yansıtır şekilde belirtin.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-177">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="d3fcd-178">Görev yeniden ya da yeniden, bu görev çalıştıran başladığı en son ne zaman olur.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-178">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="d3fcd-179">EndTime</span><span class="sxs-lookup"><span data-stu-id="d3fcd-179">endTime</span></span>|<span data-ttu-id="d3fcd-180">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d3fcd-180">DateTime</span></span>|<span data-ttu-id="d3fcd-181">Hangi görev tamamlandı süre.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-181">The time at which the task completed.</span></span>|
|<span data-ttu-id="d3fcd-182">exitCode</span><span class="sxs-lookup"><span data-stu-id="d3fcd-182">exitCode</span></span>|<span data-ttu-id="d3fcd-183">Int32</span><span class="sxs-lookup"><span data-stu-id="d3fcd-183">Int32</span></span>|<span data-ttu-id="d3fcd-184">Görev çıkış kodu.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-184">The exit code of the task.</span></span>|
|<span data-ttu-id="d3fcd-185">retryCount</span><span class="sxs-lookup"><span data-stu-id="d3fcd-185">retryCount</span></span>|<span data-ttu-id="d3fcd-186">Int32</span><span class="sxs-lookup"><span data-stu-id="d3fcd-186">Int32</span></span>|<span data-ttu-id="d3fcd-187">Görev Batch hizmeti tarafından denenen sayısı.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-187">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="d3fcd-188">Belirtilen MaxTaskRetryCount kadar bir sıfır olmayan çıkış kodu ile bulunup bulunmadığını görev denenir.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-188">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="d3fcd-189">requeueCount</span><span class="sxs-lookup"><span data-stu-id="d3fcd-189">requeueCount</span></span>|<span data-ttu-id="d3fcd-190">Int32</span><span class="sxs-lookup"><span data-stu-id="d3fcd-190">Int32</span></span>|<span data-ttu-id="d3fcd-191">Batch hizmeti tarafından bir kullanıcı isteğin sonucu olarak görev yeniden kuyruğa sayısı.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-191">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="d3fcd-192">Yeniden boyutlandırma veya havuza küçültme) bir havuz (veya ne zaman işi devre dışı bırakılıyor, kullanıcı kullanıcı kaldırır düğümleri çalışan düğümlerine görevleri belirttiğinizde çalıştırılmak üzere yeniden kuyruğa.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-192">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="d3fcd-193">Bu sayı, şu nedenlerden dolayı kaç kez görev sıraya izler.</span><span class="sxs-lookup"><span data-stu-id="d3fcd-193">This count tracks how many times the task has been requeued for these reasons.</span></span>|
