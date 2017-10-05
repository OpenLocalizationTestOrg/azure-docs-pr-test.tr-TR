---
title: "Azure Batch görev başarısız olay | Microsoft Docs"
description: "Toplu Görev başvurusunu olay başarısız."
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
ms.openlocfilehash: 08feb4ec34bb1635f8ea744b54a10b677b94ab3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="task-fail-event"></a><span data-ttu-id="1c6a3-103">Görev başarısız olayı</span><span class="sxs-lookup"><span data-stu-id="1c6a3-103">Task fail event</span></span>

 <span data-ttu-id="1c6a3-104">Bu olay, bir hata ile bir görev tamamlandıktan sonra yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-104">This event is emitted when a task completes with a failure.</span></span> <span data-ttu-id="1c6a3-105">Şu anda tüm sıfır olmayan çıkış kodları hata olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-105">Currently all nonzero exit codes are considered failures.</span></span> <span data-ttu-id="1c6a3-106">Bu olay yayılan *ek olarak* bir görevi tamamlamak olay ve bir görev başarısız olduğunda algılamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-106">This event will be emitted *in addition to* a task complete event and can be used to detect when a task has failed.</span></span>


 <span data-ttu-id="1c6a3-107">Aşağıdaki örnek, bir görevin başarısız olay gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-107">The following example shows the body of a task fail event.</span></span>

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
        "exitCode": 1,
        "retryCount": 2,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="1c6a3-108">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1c6a3-108">Element name</span></span>|<span data-ttu-id="1c6a3-109">Tür</span><span class="sxs-lookup"><span data-stu-id="1c6a3-109">Type</span></span>|<span data-ttu-id="1c6a3-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="1c6a3-110">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1c6a3-111">İş kimliği</span><span class="sxs-lookup"><span data-stu-id="1c6a3-111">jobId</span></span>|<span data-ttu-id="1c6a3-112">Dize</span><span class="sxs-lookup"><span data-stu-id="1c6a3-112">String</span></span>|<span data-ttu-id="1c6a3-113">Görevi içeren işi kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-113">The id of the job containing the task.</span></span>|
|<span data-ttu-id="1c6a3-114">id</span><span class="sxs-lookup"><span data-stu-id="1c6a3-114">id</span></span>|<span data-ttu-id="1c6a3-115">Dize</span><span class="sxs-lookup"><span data-stu-id="1c6a3-115">String</span></span>|<span data-ttu-id="1c6a3-116">Görev kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-116">The id of the task.</span></span>|
|<span data-ttu-id="1c6a3-117">taskType</span><span class="sxs-lookup"><span data-stu-id="1c6a3-117">taskType</span></span>|<span data-ttu-id="1c6a3-118">Dize</span><span class="sxs-lookup"><span data-stu-id="1c6a3-118">String</span></span>|<span data-ttu-id="1c6a3-119">Görev türü.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-119">The type of the task.</span></span> <span data-ttu-id="1c6a3-120">Bu, her bir iş yöneticisi görevi olduğunu gösteren'JobManager ' veya 'kullanıcı bir iş yöneticisi görevi değil belirten' olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-120">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="1c6a3-121">Bu olay, iş hazırlama görevleri, iş sürüm görevleri veya başlangıç görevleri için gösterilen değil.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-121">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="1c6a3-122">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="1c6a3-122">systemTaskVersion</span></span>|<span data-ttu-id="1c6a3-123">Int32</span><span class="sxs-lookup"><span data-stu-id="1c6a3-123">Int32</span></span>|<span data-ttu-id="1c6a3-124">Bir görev iç yeniden deneme sayacı budur.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-124">This is the internal retry counter on a task.</span></span> <span data-ttu-id="1c6a3-125">Dahili olarak Batch hizmeti geçici sorunlar için hesap için bir görevi yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-125">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="1c6a3-126">Bu sorunları iç zamanlama hatalar içerebilir veya kurtarma girişimleri işlem düğümleri hatalı bir durumda.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-126">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="1c6a3-127">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="1c6a3-127">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="1c6a3-128">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="1c6a3-128">Complex Type</span></span>|<span data-ttu-id="1c6a3-129">İşlem düğümünde görevin çalıştırıldığı hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-129">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="1c6a3-130">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="1c6a3-130">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="1c6a3-131">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="1c6a3-131">Complex Type</span></span>|<span data-ttu-id="1c6a3-132">Görevi birden çok işlem düğümleri gerektiren çok örnekli görev olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-132">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="1c6a3-133">Bkz: [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-133">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="1c6a3-134">kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="1c6a3-134">constraints</span></span>](#constraints)|<span data-ttu-id="1c6a3-135">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="1c6a3-135">Complex Type</span></span>|<span data-ttu-id="1c6a3-136">Bu görev için geçerli yürütme kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-136">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="1c6a3-137">executionInfo</span><span class="sxs-lookup"><span data-stu-id="1c6a3-137">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="1c6a3-138">Karmaşık türü</span><span class="sxs-lookup"><span data-stu-id="1c6a3-138">Complex Type</span></span>|<span data-ttu-id="1c6a3-139">Görevin yürütülmesi hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-139">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="1c6a3-140"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="1c6a3-140"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="1c6a3-141">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1c6a3-141">Element name</span></span>|<span data-ttu-id="1c6a3-142">Tür</span><span class="sxs-lookup"><span data-stu-id="1c6a3-142">Type</span></span>|<span data-ttu-id="1c6a3-143">Notlar</span><span class="sxs-lookup"><span data-stu-id="1c6a3-143">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1c6a3-144">poolId</span><span class="sxs-lookup"><span data-stu-id="1c6a3-144">poolId</span></span>|<span data-ttu-id="1c6a3-145">Dize</span><span class="sxs-lookup"><span data-stu-id="1c6a3-145">String</span></span>|<span data-ttu-id="1c6a3-146">Görevin çalıştırıldığı havuzun kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-146">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="1c6a3-147">nodeId</span><span class="sxs-lookup"><span data-stu-id="1c6a3-147">nodeId</span></span>|<span data-ttu-id="1c6a3-148">Dize</span><span class="sxs-lookup"><span data-stu-id="1c6a3-148">String</span></span>|<span data-ttu-id="1c6a3-149">Görevin çalıştırıldığı düğümün kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-149">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="1c6a3-150"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="1c6a3-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="1c6a3-151">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1c6a3-151">Element name</span></span>|<span data-ttu-id="1c6a3-152">Tür</span><span class="sxs-lookup"><span data-stu-id="1c6a3-152">Type</span></span>|<span data-ttu-id="1c6a3-153">Notlar</span><span class="sxs-lookup"><span data-stu-id="1c6a3-153">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1c6a3-154">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="1c6a3-154">numberOfInstances</span></span>|<span data-ttu-id="1c6a3-155">Int32</span><span class="sxs-lookup"><span data-stu-id="1c6a3-155">Int32</span></span>|<span data-ttu-id="1c6a3-156">Görevin gerektirdiği işlem düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-156">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="1c6a3-157"><a name="constraints"></a>kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="1c6a3-157"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="1c6a3-158">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1c6a3-158">Element name</span></span>|<span data-ttu-id="1c6a3-159">Tür</span><span class="sxs-lookup"><span data-stu-id="1c6a3-159">Type</span></span>|<span data-ttu-id="1c6a3-160">Notlar</span><span class="sxs-lookup"><span data-stu-id="1c6a3-160">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1c6a3-161">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="1c6a3-161">maxTaskRetryCount</span></span>|<span data-ttu-id="1c6a3-162">Int32</span><span class="sxs-lookup"><span data-stu-id="1c6a3-162">Int32</span></span>|<span data-ttu-id="1c6a3-163">Maksimum görev yeniden sayısı.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-163">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="1c6a3-164">Çıkış kodu sıfır değilse toplu işlem hizmeti görevi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-164">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="1c6a3-165">Bu değer özellikle yeniden deneme sayısını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-165">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="1c6a3-166">Toplu işlem hizmeti görevi bir kez dener ve bu sınıra kadar daha sonra yeniden deneyebilir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-166">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="1c6a3-167">Örneğin, en fazla yeniden deneme sayısı 3, toplu çalıştığında bir görevin en fazla ise 4 (bir ilk deneyin ve 3 yeniden denemeyi) zaman.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-167">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="1c6a3-168">En fazla yeniden deneme sayısının 0 olması durumunda toplu işlem hizmetinin görevleri yeniden denemez.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-168">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="1c6a3-169">En fazla yeniden deneme sayısı -1 ise, Batch hizmeti görevleri sınır olmaksızın yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-169">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="1c6a3-170">Varsayılan değer 0 (yeniden deneme)'dır.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-170">The default value is 0 (no retries).</span></span>|


###  <span data-ttu-id="1c6a3-171"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="1c6a3-171"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="1c6a3-172">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="1c6a3-172">Element name</span></span>|<span data-ttu-id="1c6a3-173">Tür</span><span class="sxs-lookup"><span data-stu-id="1c6a3-173">Type</span></span>|<span data-ttu-id="1c6a3-174">Notlar</span><span class="sxs-lookup"><span data-stu-id="1c6a3-174">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1c6a3-175">startTime</span><span class="sxs-lookup"><span data-stu-id="1c6a3-175">startTime</span></span>|<span data-ttu-id="1c6a3-176">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="1c6a3-176">DateTime</span></span>|<span data-ttu-id="1c6a3-177">Görev çalıştıran başladığı zaman.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-177">The time at which the task started running.</span></span> <span data-ttu-id="1c6a3-178">'Çalışıyor' karşılık gelen **çalıştıran** görev kaynak dosyaları veya uygulama paketleri belirtiyorsa, başlangıç saati görev başladığı indirilirken veya bunlar dağıtma zaman yansıtır şekilde belirtin.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-178">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="1c6a3-179">Görev yeniden ya da yeniden, bu görev çalıştıran başladığı en son ne zaman olur.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-179">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="1c6a3-180">EndTime</span><span class="sxs-lookup"><span data-stu-id="1c6a3-180">endTime</span></span>|<span data-ttu-id="1c6a3-181">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="1c6a3-181">DateTime</span></span>|<span data-ttu-id="1c6a3-182">Hangi görev tamamlandı süre.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-182">The time at which the task completed.</span></span>|
|<span data-ttu-id="1c6a3-183">exitCode</span><span class="sxs-lookup"><span data-stu-id="1c6a3-183">exitCode</span></span>|<span data-ttu-id="1c6a3-184">Int32</span><span class="sxs-lookup"><span data-stu-id="1c6a3-184">Int32</span></span>|<span data-ttu-id="1c6a3-185">Görev çıkış kodu.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-185">The exit code of the task.</span></span>|
|<span data-ttu-id="1c6a3-186">retryCount</span><span class="sxs-lookup"><span data-stu-id="1c6a3-186">retryCount</span></span>|<span data-ttu-id="1c6a3-187">Int32</span><span class="sxs-lookup"><span data-stu-id="1c6a3-187">Int32</span></span>|<span data-ttu-id="1c6a3-188">Görev Batch hizmeti tarafından denenen sayısı.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-188">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="1c6a3-189">Belirtilen MaxTaskRetryCount kadar bir sıfır olmayan çıkış kodu ile bulunup bulunmadığını görev denenir.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-189">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="1c6a3-190">requeueCount</span><span class="sxs-lookup"><span data-stu-id="1c6a3-190">requeueCount</span></span>|<span data-ttu-id="1c6a3-191">Int32</span><span class="sxs-lookup"><span data-stu-id="1c6a3-191">Int32</span></span>|<span data-ttu-id="1c6a3-192">Batch hizmeti tarafından bir kullanıcı isteğin sonucu olarak görev yeniden kuyruğa sayısı.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-192">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="1c6a3-193">Yeniden boyutlandırma veya havuza küçültme) bir havuz (veya ne zaman işi devre dışı bırakılıyor, kullanıcı kullanıcı kaldırır düğümleri çalışan düğümlerine görevleri belirttiğinizde çalıştırılmak üzere yeniden kuyruğa.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-193">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="1c6a3-194">Bu sayı, şu nedenlerden dolayı kaç kez görev sıraya izler.</span><span class="sxs-lookup"><span data-stu-id="1c6a3-194">This count tracks how many times the task has been requeued for these reasons.</span></span>|
