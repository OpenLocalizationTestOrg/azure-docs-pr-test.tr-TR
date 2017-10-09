---
title: "aaaUse görev bağımlılıkları toorun görevler bağlı diğer görevler - Azure Batch hello tamamlanmasından | Microsoft Docs"
description: "MapReduce stili ve benzer büyük veri işleme ile ilgili diğer görevler hello tamamlanmasından bağımlı görevler oluşturma Azure Batch iş yükleri."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="4847f-103">Görev bağımlılıkları diğer görevlere bağlı toorun görevler oluşturma</span><span class="sxs-lookup"><span data-stu-id="4847f-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="4847f-104">Yalnızca bir üst görev tamamlandıktan sonra görev bağımlılıkları toorun bir görevi veya görev kümesini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="4847f-105">Görev bağımlılıkları yararlı olduğu bazı senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4847f-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="4847f-106">MapReduce stili iş yükleri hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="4847f-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="4847f-107">İşleri, veri işleme görevlerini yönlendirilmiş Çevrimsiz grafik (DAG) ifade edilebilir.</span><span class="sxs-lookup"><span data-stu-id="4847f-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="4847f-108">Her görevin nerede Hello sonraki görev başlamadan önce tamamlamanız gerekir ön işleme ve sonrası işleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="4847f-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="4847f-109">Aşağı Akış görevleri Yukarı Akış görevleri hello çıktısını bağımlı diğer işler.</span><span class="sxs-lookup"><span data-stu-id="4847f-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="4847f-110">Toplu görev bağımlılıkları ile bir veya daha fazla üst görevleri hello tamamlandıktan sonra işlem düğümlerinde yürütülmesi için zamanlanmış görevler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="4847f-111">Örneğin, ayrı, paralel görevler içeren bir 3B film her karesini işleyen bir iş oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="4847f-112">Merhaba son görev--hello "Birleştirme görev"--hello tam film yalnızca çerçeveler çizilir hello tüm çerçeveler birleştirmeler başarıyla çizilir.</span><span class="sxs-lookup"><span data-stu-id="4847f-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="4847f-113">Yalnızca hello üst görevi başarıyla tamamlandıktan sonra varsayılan olarak, bağımlı görevler çalıştırılmak üzere zamanlandı.</span><span class="sxs-lookup"><span data-stu-id="4847f-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="4847f-114">Bir bağımlılık eylem toooverride hello varsayılan davranışı belirtin ve hello üst görevi başarısız olduğunda görev çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4847f-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="4847f-115">Merhaba bkz [bağımlılık Eylemler](#dependency-actions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="4847f-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="4847f-116">Diğer görevleri birebir veya bire çok ilişkide bağımlı görevler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="4847f-117">Burada hello tamamlama görevleri görev kimlikleri belirtilen bir aralıkta Grubu'nun bir görevin bağlı bir aralık bağımlılık de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="4847f-118">Bu üç temel senaryodan toocreate çok-çok ilişkileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="4847f-119">Görev bağımlılıkları Batch .NET ile</span><span class="sxs-lookup"><span data-stu-id="4847f-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="4847f-120">Bu makalede, nasıl kullanarak tooconfigure görev bağımlılıkları hello aşağıdakiler ele [Batch .NET] [ net_msdn] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="4847f-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="4847f-121">İlk nasıl çok gösteriyoruz[görev bağımlılığı etkinleştirmek](#enable-task-dependencies) , işlerini ve nasıl çok göstermek[görev bağımlılıkları ile yapılandırma](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="4847f-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="4847f-122">Merhaba üst başarısız olursa bir bağımlılık eylem toorun bağımlı nasıl toospecify görevler de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4847f-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="4847f-123">Son olarak, hello aşağıdakiler ele [bağımlılık senaryolarına](#dependency-scenarios) toplu destekleyen.</span><span class="sxs-lookup"><span data-stu-id="4847f-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="4847f-124">Görev bağımlılıkları etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4847f-124">Enable task dependencies</span></span>
<span data-ttu-id="4847f-125">Batch uygulamanızda toouse görev bağımlılıkları, öncelikle hello iş toouse görev bağımlılıkları yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4847f-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="4847f-126">Batch .NET içinde etkinleştirmeden, [CloudJob] [ net_cloudjob] ayarlayarak kendi [UsesTaskDependencies] [ net_usestaskdependencies] özelliği çok`true`:</span><span class="sxs-lookup"><span data-stu-id="4847f-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="4847f-127">Önceki kod parçacığını hello "batchClient" Merhaba örneği olan [BatchClient] [ net_batchclient] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4847f-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="4847f-128">Bağımlı görevler oluşturma</span><span class="sxs-lookup"><span data-stu-id="4847f-128">Create dependent tasks</span></span>
<span data-ttu-id="4847f-129">bir veya daha fazla üst görevleri hello tamamlanmasından bağlıdır bir görev toocreate, diğer görevler, görev "bağlıdır" Merhaba hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="4847f-130">Batch .NET içinde hello yapılandırma [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] hello örneği özelliğiyle [Github_samples] [ net_taskdependencies] sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4847f-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="4847f-131">Bu kod parçacığını görev kimliği "Çiçekler" bağımlı bir görev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4847f-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="4847f-132">Merhaba "Çiçekler" görev görevlere "Yağmur" ve "Sun" bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4847f-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="4847f-133">Görev "Çiçekler" bir işlem düğümünde zamanlanmış toorun yalnızca "Yağmur" ve "Sun" tamamladınız görevleri sonra olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4847f-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="4847f-134">Bir görev hello olduğunda toobe başarıyla tamamlandı olarak kabul edilir **tamamlandı** durumu ve kendi **çıkış kodu** olan `0`.</span><span class="sxs-lookup"><span data-stu-id="4847f-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="4847f-135">Batch .NET içinde yani bir [CloudTask][net_cloudtask].[ Durumu] [ net_taskstate] özellik değerinin `Completed` ve CloudTask'ın hello [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] özellik değeri `0`.</span><span class="sxs-lookup"><span data-stu-id="4847f-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="4847f-136">Bağımlılık senaryoları</span><span class="sxs-lookup"><span data-stu-id="4847f-136">Dependency scenarios</span></span>
<span data-ttu-id="4847f-137">Azure Batch kullanabileceğiniz üç temel görev bağımlılık senaryo vardır: birebir, bir çok ve görev kimliği aralığı bağımlılık.</span><span class="sxs-lookup"><span data-stu-id="4847f-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="4847f-138">Bu birleşik tooprovide dördüncü bir senaryo, çok-olabilir.</span><span class="sxs-lookup"><span data-stu-id="4847f-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="4847f-139">Senaryo&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="4847f-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="4847f-140">Örnek</span><span class="sxs-lookup"><span data-stu-id="4847f-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="4847f-141">Bire bir</span><span class="sxs-lookup"><span data-stu-id="4847f-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="4847f-142">*Görevb* bağlıdır *Göreva*</span><span class="sxs-lookup"><span data-stu-id="4847f-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="4847f-143">*Görevb* kadar yürütülmek zamanlanmaz *Göreva* başarıyla tamamlandı</span><span class="sxs-lookup"><span data-stu-id="4847f-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="4847f-144">![Diyagram: bire bir görev bağımlılığı][1]</span><span class="sxs-lookup"><span data-stu-id="4847f-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="4847f-145">Bir çok</span><span class="sxs-lookup"><span data-stu-id="4847f-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="4847f-146">*görevC* hem *görevA* hem de *görevB*’ye bağlıdır</span><span class="sxs-lookup"><span data-stu-id="4847f-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="4847f-147">*Görevc* her ikisi de kadar yürütülmek zamanlanmaz *Göreva* ve *Görevb* başarıyla tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="4847f-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="4847f-148">![Diyagram: bir çok görev bağımlılığı][2]</span><span class="sxs-lookup"><span data-stu-id="4847f-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="4847f-149">Görev Kimliği aralığı</span><span class="sxs-lookup"><span data-stu-id="4847f-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="4847f-150">*Görevd* bir dizi göreve bağlıdır</span><span class="sxs-lookup"><span data-stu-id="4847f-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="4847f-151">*Görevd* kimlikleri hello görevlerle kadar yürütülmek zamanlanmaz *1* aracılığıyla *10* başarıyla tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="4847f-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="4847f-152">![Diyagram: Görev kimliği aralığı bağımlılığı][3]</span><span class="sxs-lookup"><span data-stu-id="4847f-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="4847f-153">Oluşturabileceğiniz **çok-** burada görevlere A ve b C D, E ve F her görevleri bağlı gibi ilişkileri Bu, örneğin, paralel birkaç ölçeklendirin önişlem senaryolarında olduğu birden çok Yukarı Akış görevi hello çıktısını aşağı akış görevlerinizi bağımlı yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4847f-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="4847f-154">Yalnızca hello üst görevleri başarıyla tamamlandıktan sonra bu bölümde hello örneklerde, bağımlı bir görev çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="4847f-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="4847f-155">Bağımlı bir görev için varsayılan davranış hello davranıştır.</span><span class="sxs-lookup"><span data-stu-id="4847f-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="4847f-156">Bir bağımlılık eylem toooverride hello varsayılan davranışı belirterek üst görev başarısız olduktan sonra bağımlı görev çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="4847f-157">Merhaba bkz [bağımlılık Eylemler](#dependency-actions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="4847f-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="4847f-158">Bire bir</span><span class="sxs-lookup"><span data-stu-id="4847f-158">One-to-one</span></span>
<span data-ttu-id="4847f-159">Bire bir ilişkide bir görev hello başarılı bir üst görevin tamamlanma bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4847f-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="4847f-160">toocreate Merhaba bağımlılık, tek bir görev kimliği toohello sağlamak [Github_samples][net_taskdependencies].[ OnId] [ net_onid] hello doldurmak statik yöntemi [DependsOn] [ net_dependson] özelliği [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="4847f-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="4847f-161">Bir çok</span><span class="sxs-lookup"><span data-stu-id="4847f-161">One-to-many</span></span>
<span data-ttu-id="4847f-162">Bir-çok ilişkisi görev birden çok üst görevleri hello tamamlanmasından bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4847f-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="4847f-163">toocreate Merhaba bağımlılık, görev kimlikleri toohello koleksiyonunu sağlamak [Github_samples][net_taskdependencies].[ OnIds] [ net_onids] hello doldurmak statik yöntemi [DependsOn] [ net_dependson] özelliği [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="4847f-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="4847f-164">Görev Kimliği aralığı</span><span class="sxs-lookup"><span data-stu-id="4847f-164">Task ID range</span></span>
<span data-ttu-id="4847f-165">Üst görevleri bir dizi bir bağımlılık olarak hello hello tamamlama görevleri, kimlikleri bir aralıkta bulunan bir görev bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4847f-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="4847f-166">toocreate hello bağımlılık hello ilk sağlayın ve son kimlikleri hello aralığı toohello görev [Github_samples][net_taskdependencies].[ OnIdRange] [ net_onidrange] hello doldurmak statik yöntemi [DependsOn] [ net_dependson] özelliği [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="4847f-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4847f-167">Bağımlılıklarınız için görev kimliği aralıklarını kullandığınızda, görev kimlikleri hello aralıktaki hello *gerekir* tamsayı değerleri dize gösterimlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="4847f-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="4847f-168">Her görev hello aralıktaki hello bağımlılık başarıyla tamamlanmasını ya da çok ayarlamak eşlenen tooa bağımlılık eylem bir hata ile Tamamlanıyor karşılaması gerekir**Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="4847f-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="4847f-169">Merhaba bkz [bağımlılık Eylemler](#dependency-actions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="4847f-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="4847f-170">Bağımlılık Eylemler</span><span class="sxs-lookup"><span data-stu-id="4847f-170">Dependency actions</span></span>

<span data-ttu-id="4847f-171">Yalnızca bir üst görev başarıyla tamamlandıktan sonra varsayılan olarak, bağımlı görev veya dizi görevi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="4847f-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="4847f-172">Merhaba üst görev başarısız olsa bile, bazı senaryolarda, toorun bağımlı görevler isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="4847f-173">Bir bağımlılık eylemi belirterek hello varsayılan davranışı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="4847f-174">Bir bağımlılık eylemi bağımlı görev hello başarı veya başarısızlık hello üst görevinin durumuna göre uygun toorun olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="4847f-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="4847f-175">Örneğin, bağımlı görevi hello Yukarı Akış görevi hello tamamlanmasından verilerden bekliyor varsayalım.</span><span class="sxs-lookup"><span data-stu-id="4847f-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="4847f-176">Merhaba Yukarı Akış görevi başarısız olursa, hello bağımlı görev hala eski verileri kullanarak mümkün toorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="4847f-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="4847f-177">Bu durumda, bir bağımlılık eylemin hello bağımlı görev hello üst görev hello başarısızlığını rağmen uygun toorun belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4847f-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="4847f-178">Bir bağımlılık eylemin hello üst görev için bir çıkış koşulu temel alır.</span><span class="sxs-lookup"><span data-stu-id="4847f-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="4847f-179">Herhangi bir çıkış koşullarını izleyen hello için bir bağımlılık eylemi belirtebilirsiniz; .NET için bkz: Merhaba [ExitConditions] [ net_exitconditions] sınıfı Ayrıntılar için:</span><span class="sxs-lookup"><span data-stu-id="4847f-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="4847f-180">Ön işleme bir hata oluştuğunda.</span><span class="sxs-lookup"><span data-stu-id="4847f-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="4847f-181">Bir dosyayı karşıya yüklemeyi hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="4847f-181">When a file upload error occurs.</span></span> <span data-ttu-id="4847f-182">Merhaba görev aracılığıyla belirtilen çıkış kodu ile çıkar varsa **exitCodes** veya **exitCodeRanges**ve bir dosya karşıya yükleme hatası, hello eylemin hello çıkış kodu önceliğe tarafından belirtilen karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="4847f-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="4847f-183">Merhaba görev çıktığında hello tarafından tanımlanan bir çıkış kodu ile **ExitCodes** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4847f-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="4847f-184">Merhaba görev çıktığında hello tarafından belirtilen bir aralıkta denk bir çıkış kodu ile **ExitCodeRanges** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4847f-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="4847f-185">Başlangıç görevi tarafından tanımlanmamış bir çıkış kodu ile bulunup bulunmadığını varsayılan durumda, Hello **ExitCodes** veya **ExitCodeRanges**, veya bir ön-işleme hatası ve hello hello görev bulunup bulunmadığını **PreProcessingError**  özelliği ayarlı değil ya da hello gerekmiyorsa görev başarısız bir dosyayla hata ve hello karşıya **FileUploadError** özelliği ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="4847f-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="4847f-186">toospecify .NET, kümesi hello bağımlılık eylemde [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] hello çıkış koşulu özelliği.</span><span class="sxs-lookup"><span data-stu-id="4847f-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="4847f-187">Merhaba **DependencyAction** özelliği iki değerden birini alır:</span><span class="sxs-lookup"><span data-stu-id="4847f-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="4847f-188">Ayar hello **DependencyAction** özelliği çok**Satisfy** belirtilen bir hata ile Merhaba üst görev bulunup bulunmadığını bağımlı görevler uygun toorun olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4847f-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="4847f-189">Ayar hello **DependencyAction** özelliği çok**blok** bağımlı görevler uygun toorun olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4847f-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="4847f-190">Merhaba hello için varsayılan ayar **DependencyAction** özelliği **Satisfy** çıkış kodu 0 için ve **blok** diğer tüm çıkış koşulları için.</span><span class="sxs-lookup"><span data-stu-id="4847f-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="4847f-191">Merhaba aşağıdaki kod parçacığını ayarlar hello **DependencyAction** özelliği için bir üst görev.</span><span class="sxs-lookup"><span data-stu-id="4847f-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="4847f-192">Ön işleme bir hata ile Merhaba üst görev çıkar veya hello ile belirtilen hata kodları hello bağımlı görev engellendi.</span><span class="sxs-lookup"><span data-stu-id="4847f-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="4847f-193">Başka bir sıfır olmayan hata ile Merhaba üst görev bulunup bulunmadığını hello bağımlı uygun toorun bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="4847f-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="4847f-194">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="4847f-194">Code sample</span></span>
<span data-ttu-id="4847f-195">Merhaba [Github_samples] [ github_taskdependencies] örnek proje hello biridir [Azure Batch kod örnekleri] [ github_samples] github'da.</span><span class="sxs-lookup"><span data-stu-id="4847f-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="4847f-196">Bu Visual Studio çözümü gösterir:</span><span class="sxs-lookup"><span data-stu-id="4847f-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="4847f-197">Nasıl tooenable görev iş bağımlılığı</span><span class="sxs-lookup"><span data-stu-id="4847f-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="4847f-198">Nasıl toocreate görevler diğer görevlere bağlı</span><span class="sxs-lookup"><span data-stu-id="4847f-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="4847f-199">Tooexecute olanlar nasıl görevler üzerinde işlem düğümü havuzu oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="4847f-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4847f-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4847f-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="4847f-201">Uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="4847f-201">Application deployment</span></span>
<span data-ttu-id="4847f-202">Merhaba [uygulama paketleri](batch-application-packages.md) batch özelliği bir tooboth dağıtmak için kolay bir yolla ve görevlerinizi yürütmek hello uygulamaları işlem düğümlerini sürüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="4847f-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="4847f-203">Uygulama yükleme ve verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="4847f-203">Installing applications and staging data</span></span>
<span data-ttu-id="4847f-204">Bkz: [uygulamaların yüklenmesi ve toplu veri hazırlama işlem düğümlerini] [ forum_post] toorun görevleri düğümleriniz hazırlığı yöntemlerine genel bakış için hello Azure Batch Forumunda.</span><span class="sxs-lookup"><span data-stu-id="4847f-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="4847f-205">Hello Azure Batch ekip üyelerinin, biri tarafından bu post hello farklı şekillerde toocopy uygulamaları iyi öncü yazılır, görev giriş verilerinin ve diğer dosyaları tooyour işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="4847f-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diyagram: bire bir bağımlılık"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diyagram: bir çok bağımlılık"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diyagram: görev kimliği aralığı bağımlılığı"
