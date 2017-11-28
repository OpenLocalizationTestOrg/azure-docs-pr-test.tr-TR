---
title: "Paralel toouse aaaRun görevlerinde işlem kaynaklarını verimli bir şekilde - Azure Batch | Microsoft Docs"
description: "Azure Batch havuzundaki her düğümde daha az işlem düğümlerini ve çalışan eş zamanlı görevleri kullanarak verimliliği ve maliyetleri artırın"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="31d23-103">Toplu işlem düğümleri toomaximize kullanımını eşzamanlı olarak çalışan görevler</span><span class="sxs-lookup"><span data-stu-id="31d23-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="31d23-104">Birden fazla görev aynı anda Azure Batch havuzundaki her işlem düğümünde çalıştırarak hello havuzdaki düğümlerin daha az sayıda kaynak kullanımı en üst düzeye çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31d23-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="31d23-105">Bazı iş yükleri için bu kısa iş süreleri ve daha düşük maliyetli neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="31d23-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="31d23-106">Bir düğümün kaynakları tooa tek görev tümünün ayrılması bazı senaryolarda yararlı olsa da, bazı durumlarda bu kaynakları birden çok görevleri tooshare izin vererek yararlanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31d23-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="31d23-107">**Veri aktarımı en aza** görevleri mümkün tooshare veri olduğunda.</span><span class="sxs-lookup"><span data-stu-id="31d23-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="31d23-108">Bu senaryoda, önemli ölçüde veri aktarımı ücretlerine paylaşılan veri tooa daha az sayıda düğüm kopyalayarak azaltabilir ve her bir düğümde Paralel Görevler yürütme.</span><span class="sxs-lookup"><span data-stu-id="31d23-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="31d23-109">Bu özellikle, Hello veri toobe kopyalanan tooeach düğümü coğrafi bölgeler arasında aktarılması geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="31d23-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="31d23-110">**Bellek kullanımını en üst düzeye çıkarma** görevleri bellek, ancak yalnızca dönemlerde kısa süre ve yürütme sırasında değişken zamanlarda büyük bir miktarını ne zaman gerektirir.</span><span class="sxs-lookup"><span data-stu-id="31d23-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="31d23-111">Daha az, ancak büyük kullanan, daha fazla bellek tooefficiently düğümleriyle böyle artışlarını işlem.</span><span class="sxs-lookup"><span data-stu-id="31d23-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="31d23-112">Bu düğümler her düğümde paralel olarak çalışan birden çok görev gerekir, ancak farklı zamanlarda her görev hello düğümleri çoktur bellek yararlanmak.</span><span class="sxs-lookup"><span data-stu-id="31d23-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="31d23-113">**Düğüm sayı sınırları Azaltıcı** düğümler arası iletişimin olduğunda bir havuzu içinde gerekli.</span><span class="sxs-lookup"><span data-stu-id="31d23-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="31d23-114">Şu anda, sınırlı too50 işlem düğümleri havuzları düğümler arası iletişim için yapılandırılan içindedir.</span><span class="sxs-lookup"><span data-stu-id="31d23-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="31d23-115">Bu tür bir havuzdaki her düğüme mümkün tooexecute görevi paralel ise, görevlerin daha fazla sayıda eşzamanlı olarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="31d23-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="31d23-116">**Bir şirket içi işlem kümesi çoğaltma**, bilgi işlem ortamı tooAzure ilk taşıdığınızda gibi.</span><span class="sxs-lookup"><span data-stu-id="31d23-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="31d23-117">Geçerli şirket içi çözümünüzü işlem düğümü başına birden çok görev yürütülürse hello en fazla sayıyı artırabilirsiniz düğümü görevlerin toomore yakından yapılandırmayı yansıtmak.</span><span class="sxs-lookup"><span data-stu-id="31d23-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="31d23-118">Örnek senaryo</span><span class="sxs-lookup"><span data-stu-id="31d23-118">Example scenario</span></span>
<span data-ttu-id="31d23-119">Bir örnek tooillustrate olarak Merhaba paralel görev yürütme avantajları, görev uygulamanızı CPU ve bellek gereksinimleri karşıladığından emin düşünelim şekilde [standart\_D1](../cloud-services/cloud-services-sizes-specs.md) düğümleri yeterli.</span><span class="sxs-lookup"><span data-stu-id="31d23-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="31d23-120">Ancak, sipariş toofinish hello işinde gerekli hello zaman içinde bu düğümler 1.000 gereklidir.</span><span class="sxs-lookup"><span data-stu-id="31d23-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="31d23-121">Standart kullanmak yerine\_1 CPU çekirdeği olan D1 düğümleri kullanabilir [standart\_D14](../cloud-services/cloud-services-sizes-specs.md) 16 çekirdeğe sahip ve paralel görev yürütme etkinleştiren düğümleri.</span><span class="sxs-lookup"><span data-stu-id="31d23-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="31d23-122">Bu nedenle, *16 kez daha az düğümü* 63 gerekli olacak yalnızca--1.000 düğümleri yerine kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="31d23-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="31d23-123">Büyük uygulama dosyaları veya başvuru verileri her düğüm için gerekirse, hello veri kopyalanan tooonly 16 düğüme olduğundan ek olarak, iş süresi ve verimlilik yeniden geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="31d23-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="31d23-124">Paralel görev yürütme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="31d23-124">Enable parallel task execution</span></span>
<span data-ttu-id="31d23-125">Paralel görev yürütme için işlem düğümlerine hello havuzu düzeyinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="31d23-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="31d23-126">Merhaba Batch .NET kitaplığı ile Merhaba ayarlamak [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] bir havuz oluşturduğunuzda özelliği.</span><span class="sxs-lookup"><span data-stu-id="31d23-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="31d23-127">Merhaba Batch REST API'si kullanıyorsanız, hello ayarlamak [maxTasksPerNode] [ rest_addpool] havuzu oluşturma sırasında hello istek gövdesindeki öğesi.</span><span class="sxs-lookup"><span data-stu-id="31d23-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="31d23-128">Azure Batch tooset toofour kez (4 x) hello düğüm çekirdek sayısı düğümü başına en fazla görevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="31d23-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="31d23-129">Örneğin, hello kullanırsanız havuz boyutu "Büyük" (dört çekirdek), düğümler ile sonra yapılandırılır `maxTasksPerNode` too16 ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="31d23-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="31d23-130">Merhaba her hello düğümü boyutları için çekirdek sayısı hakkında daha fazla bilgi için bkz: [Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="31d23-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="31d23-131">Hizmet sınırları hakkında daha fazla bilgi için bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="31d23-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="31d23-132">Hesap hello içine emin tootake olması `maxTasksPerNode` değeri, yapısı oluştururken bir [otomatik ölçeklendirme formülü] [ enable_autoscaling] havuzunuz için.</span><span class="sxs-lookup"><span data-stu-id="31d23-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="31d23-133">Örneğin, veren bir formül `$RunningTasks` önemli ölçüde görevleri düğümü başına bir artış tarafından etkilenebilir.</span><span class="sxs-lookup"><span data-stu-id="31d23-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="31d23-134">Bkz: [ölçek işlem düğümlerini Azure Batch havuzunda otomatik olarak](batch-automatic-scaling.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="31d23-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="31d23-135">Dağıtım görevleri</span><span class="sxs-lookup"><span data-stu-id="31d23-135">Distribution of tasks</span></span>
<span data-ttu-id="31d23-136">Bir havuzdaki işlem düğümleri Hello görevler eşzamanlı olarak yürütebilir hello havuzdaki hello düğümleri dağıtılmış hello görevleri toobe istediğiniz önemli toospecify olur.</span><span class="sxs-lookup"><span data-stu-id="31d23-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="31d23-137">Hello kullanarak [CloudPool.TaskSchedulingPolicy] [ task_schedule] özelliği, görevler ("yayılmak") hello havuzdaki tüm düğümlere eşit olarak atanmalıdır belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31d23-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="31d23-138">Veya ("sevk") hello havuzdaki tooanother düğüme atanan görevleri önce mümkün olduğunca çok görevleri tooeach düğümü atanmalıdır belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31d23-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="31d23-139">Bu özellik nasıl değerlidir örnek olarak, hello havuzu göz önünde bulundurun [standart\_D14](../cloud-services/cloud-services-sizes-specs.md) ile yapılandırılmış düğümlerin (Merhaba Yukarıdaki örnekteki) bir [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 16 değeri.</span><span class="sxs-lookup"><span data-stu-id="31d23-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="31d23-140">Merhaba, [CloudPool.TaskSchedulingPolicy] [ task_schedule] ile yapılandırılmış bir [ComputeNodeFillType] [ fill_type] , *paketi*, her düğümün tüm 16 çekirdeğe kullanımını en üst düzeye ve izin bir [otomatik ölçeklendirmeyi havuzu](batch-automatic-scaling.md) tooprune kullanılmayan düğümleri hello havuzundan (düğümler atanmış herhangi bir görevi olmadan).</span><span class="sxs-lookup"><span data-stu-id="31d23-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="31d23-141">Bu kaynak kullanımını en aza indirir ve para kaydeder.</span><span class="sxs-lookup"><span data-stu-id="31d23-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="31d23-142">Batch .NET örnek</span><span class="sxs-lookup"><span data-stu-id="31d23-142">Batch .NET example</span></span>
<span data-ttu-id="31d23-143">Bu [Batch .NET] [ api_net] API kod parçacığını en fazla düğüm başına dört görevler dört büyük düğümleri içeren bir havuzu isteği toocreate gösterir.</span><span class="sxs-lookup"><span data-stu-id="31d23-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="31d23-144">Bir görev görevleri önceki tooassigning görevleri tooanother düğümle hello havuzdaki her düğüm doldurur ilke zamanlama belirtir.</span><span class="sxs-lookup"><span data-stu-id="31d23-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="31d23-145">Merhaba Batch .NET API'si kullanarak havuzları ekleme ile ilgili daha fazla bilgi için bkz: [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="31d23-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="31d23-146">Batch REST örneği</span><span class="sxs-lookup"><span data-stu-id="31d23-146">Batch REST example</span></span>
<span data-ttu-id="31d23-147">Bu [Batch REST] [ api_rest] API parçacığı en fazla düğüm başına dört görevleri iki büyük düğümleri içeren bir havuzu isteği toocreate gösterir.</span><span class="sxs-lookup"><span data-stu-id="31d23-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="31d23-148">Merhaba REST API kullanarak havuzları ekleme ile ilgili daha fazla bilgi için bkz: [bir havuz tooan hesabı eklemek][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="31d23-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="31d23-149">Merhaba ayarlayabilirsiniz `maxTasksPerNode` öğesi ve [MaxTasksPerComputeNode] [ maxtasks_net] havuzu oluşturma zamanında yalnızca özelliği.</span><span class="sxs-lookup"><span data-stu-id="31d23-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="31d23-150">Bir havuzu zaten oluşturulduktan sonra bunlar değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="31d23-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="31d23-151">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="31d23-151">Code sample</span></span>
<span data-ttu-id="31d23-152">Merhaba [ParallelNodeTasks] [ parallel_tasks_sample] GitHub projede hello hello kullanımını göstermektedir [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] özelliği.</span><span class="sxs-lookup"><span data-stu-id="31d23-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="31d23-153">Merhaba bu C# konsol uygulaması kullanan [Batch .NET] [ api_net] kitaplığı toocreate havuzu bir veya daha fazla ile işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="31d23-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="31d23-154">Bu düğümler toosimulate değişken yük yapılandırılabilir bir dizi görevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="31d23-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="31d23-155">Merhaba uygulamasından çıkışın, her görevin hangi düğümlerin yürütülen belirtir.</span><span class="sxs-lookup"><span data-stu-id="31d23-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="31d23-156">Merhaba uygulaması ayrıca hello iş parametrelerini ve süresi bir özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="31d23-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="31d23-157">Merhaba Özet hello örnek uygulamasının iki farklı çalıştırmalarını hello çıktısını kısmı aşağıda yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="31d23-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="31d23-158">Hello ilk yürütme hello örnek uygulamasının hello havuzunu ve her düğüm, bir görevin hello varsayılan ayar olarak tek bir düğüm ile hello iş süresi boyunca 30 dakikadır gösterir.</span><span class="sxs-lookup"><span data-stu-id="31d23-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="31d23-159">Merhaba iş süresi önemli bir düşüş ikinci hello örnek gösterir çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="31d23-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="31d23-160">Paralel görev yürütme toocomplete hello işi için neredeyse hello zaman bir Çeyrek içinde sağlayan düğüm başına dört görevlerle Hello havuzu yapılandırılmış olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="31d23-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="31d23-161">Merhaba iş süreleri hello özetleri yukarıdaki içinde havuzu oluşturma zamanı içermez.</span><span class="sxs-lookup"><span data-stu-id="31d23-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="31d23-162">Her hello işlerin yukarıdaki işlem düğümleri bundan hello oluşturulan gönderilen toopreviously havuzları edildi *boşta* gönderme zaman durum.</span><span class="sxs-lookup"><span data-stu-id="31d23-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="31d23-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31d23-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="31d23-164">Batch Explorer ısı Haritası</span><span class="sxs-lookup"><span data-stu-id="31d23-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="31d23-165">Merhaba [Azure Batch Gezgini][batch_explorer], hello Azure Batch birini [örnek uygulamaları][github_samples], içeren bir *ısıHaritası* görev yürütme görselleştirme sağlayan özelliktir.</span><span class="sxs-lookup"><span data-stu-id="31d23-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="31d23-166">Ne zaman, yürütme hello [ParallelTasks] [ parallel_tasks_sample] kullanabileceğiniz örnek uygulama hello ısı Haritası özelliği tooeasily her düğümde Paralel Görevler hello yürütülmesi görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="31d23-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Batch Explorer ısı Haritası][1]

<span data-ttu-id="31d23-168">*Şu anda yürütülmekte olan dört görevleri her düğüm ile dört düğüm havuzu gösteren batch Explorer ısı Haritası*</span><span class="sxs-lookup"><span data-stu-id="31d23-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
