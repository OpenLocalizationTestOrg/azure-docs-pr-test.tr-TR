---
title: "aaaRun Azure Batch iş yükleri uygun maliyetli düşük öncelikli vm'lerde (Önizleme) | Microsoft Docs"
description: "Azure Batch iş yükünü nasıl tooprovision düşük öncelikli sanal makineleri tooreduce hello maliyet öğrenin."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="117fc-103">Düşük öncelikli sanal makineleri toplu (Önizleme) ile kullanma</span><span class="sxs-lookup"><span data-stu-id="117fc-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="117fc-104">Azure Batch Batch iş yükü düşük versiyonda öncelik sanal makineleri (VM'ler) tooreduce hello maliyeti sunar.</span><span class="sxs-lookup"><span data-stu-id="117fc-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="117fc-105">Düşük öncelikli sanal makineleri de ekonomiktir işlem gücü, büyük bir miktarını sağlayarak, toplu iş yüklerinin yeni türleri mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="117fc-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="117fc-106">Düşük öncelikli sanal makineleri Azure'da fazlalık kapasite yararlanın.</span><span class="sxs-lookup"><span data-stu-id="117fc-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="117fc-107">Düşük öncelikli sanal makineleri, havuzlarınızı belirttiğinizde, Azure Batch bu fazlalık kullanılabilir olduğunda otomatik olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="117fc-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="117fc-108">düşük öncelikli sanal makineleri kullanma hello kolaylığını hiçbir fazlalık kapasite Azure içinde kullanılabilir olduğunda bu VM'lerin etkisiz ' dir.</span><span class="sxs-lookup"><span data-stu-id="117fc-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="117fc-109">Bu nedenle, düşük öncelikli sanal makineleri belirli türde bir iş yükleri için en uygun.</span><span class="sxs-lookup"><span data-stu-id="117fc-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="117fc-110">Düşük öncelikli sanal makineleri toplu ve burada hello iş tamamlanma zamanı esnek ve hello iş üzerinde birçok VM dağıtılmış zaman uyumsuz işleme iş yükleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="117fc-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="117fc-111">Düşük öncelikli sanal makineleri özel VM'ler önemli ölçüde daha az pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="117fc-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="117fc-112">Fiyatlandırma ayrıntıları için bkz: [Batch fiyatlandırması](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="117fc-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="117fc-113">Düşük öncelikli sanal makineleri için bir ek tartışma hello blog yayını duyurusuna bakın: [toplu bir hello fiyat kesir bilgi işlem](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="117fc-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="117fc-114">Düşük öncelikli sanal makineleri şu anda önizlemede ve yalnızca toplu işlemde çalışan iş yükleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="117fc-115">Düşük öncelikli VM'ler için kullanım örnekleri</span><span class="sxs-lookup"><span data-stu-id="117fc-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="117fc-116">Düşük öncelikli sanal makineleri Hello özelliklerini göz önüne alındığında, hangi iş yüklerini kullanabilir ve bunları kullanamazsınız?</span><span class="sxs-lookup"><span data-stu-id="117fc-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="117fc-117">Genel olarak, işleri birçok paralel görevlere bozuk veya çıkışı ölçeği ve üzerinde birçok VM dağıtılan birçok iş iyi bir tercihtir toplu işleme iş yüklerinin olduğunu.</span><span class="sxs-lookup"><span data-stu-id="117fc-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="117fc-118">Azure, uygun işlerinde fazlalık kapasite kullanımını toomaximize çıkışı ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="117fc-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="117fc-119">Bazen VM'ler kullanılabilir durumda olmayabilir veya, işleri için sınırlı kapasite neden olur ve tootask kesinti ve tekrar bölümlerini etkisiz.</span><span class="sxs-lookup"><span data-stu-id="117fc-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="117fc-120">İşlerini, bu nedenle toorun sürebilir hello zamanında esnek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="117fc-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="117fc-121">İşlerini uzun görevlerle kesintiye varsa daha etkilenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="117fc-122">Uzun süre çalışan bunlar yürütme gibi görevleri denetim noktası oluşturma toosave ilerleme uygulamak ise, ardından kesinti etkisini çok daha az olabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="117fc-123">Kesinti Hello etkisini çok daha az olduğu gibi kısa yürütme süreleri görevlerle toowork en iyi olan düşük öncelikli VM'ler eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="117fc-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="117fc-124">Uzun süre çalışan birden çok VM kullanan MPI işlerini uygun toouse olmayan bir etkisiz VM düşük öncelikli VM'ler büyük olasılıkla sağlama toohello tüm işi yeniden çalıştırmak toobe sahip olur.</span><span class="sxs-lookup"><span data-stu-id="117fc-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="117fc-125">Düşük öncelikli VM'ler durumlarda uygun toouse bazı toplu işlem örnekleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="117fc-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="117fc-126">**Geliştirme ve test**: özel olarak, büyük ölçekli çözümleri geliştirdiğinizde, önemli tasarrufları alırlar.</span><span class="sxs-lookup"><span data-stu-id="117fc-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="117fc-127">Sınama tüm türleri yararlanabilirsiniz, ancak büyük ölçekli yük test etme ve gerileme sınaması harika kullanır.</span><span class="sxs-lookup"><span data-stu-id="117fc-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="117fc-128">**İsteğe bağlı kapasite ekleme**: düşük öncelikli sanal makineleri, normal özel VM'ler - tamamlamak için kullanılabilir kullanılabilir olduğunda, işleri ölçeklendirmek ve bu nedenle daha hızlı tamamlamak için daha düşük maliyetli; VM'ler kullanılabilir hello taban ayrılmış seçtiğinizde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="117fc-129">**Esnek iş yürütme süresi**: hello zaman işlerinde esneklik ise toocomplete, sahip sonra kapasite olası bırakmaları izin; Bununla birlikte, hello ile düşük öncelikli sanal makineleri işleri eklenmesi sık daha hızlı ve daha düşük maliyetli bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="117fc-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="117fc-130">Batch havuzları, düşük öncelikli sanal makineleri hello esneklik bağlı olarak birkaç şekilde, iş yürütme süresi yapılandırılan toouse olabilir:</span><span class="sxs-lookup"><span data-stu-id="117fc-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="117fc-131">Düşük öncelikli sanal makineleri yalnızca bir havuzda kullanılabilir ve toplu herhangi preempted kapasite kullanılabilir olduğunda yalnızca kurtarır.</span><span class="sxs-lookup"><span data-stu-id="117fc-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="117fc-132">Düşük öncelikli yalnızca VM'ler kullanılır gibi hello ucuz yolu tooexecute işleri budur.</span><span class="sxs-lookup"><span data-stu-id="117fc-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="117fc-133">Düşük öncelikli sanal makineleri, sabit bir taban çizgisi özel VM'ler ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="117fc-134">Merhaba ayrılmış sanal sabit sayıda iş İleri aşamalara her zaman bazı kapasite tookeep olan sağlar.</span><span class="sxs-lookup"><span data-stu-id="117fc-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="117fc-135">Böylece ucuz düşük öncelikli sanal makineleri yalnızca kullanılabilir olduğunda kullanılır, ancak adanmış bir hello tam fiyatlı VM'ler gerektiğinde tookeep kapasite kullanılabilir tookeep hello işleri en düşük düzeyde yukarı ölçeklendirilemez ayrılmış ve düşük öncelikli sanal makineleri, dinamik karışımı olabilir İleri aşamalara.</span><span class="sxs-lookup"><span data-stu-id="117fc-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="117fc-136">Düşük öncelikli VM'ler için toplu desteği</span><span class="sxs-lookup"><span data-stu-id="117fc-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="117fc-137">Azure Batch kolay tooconsume ve düşük öncelikli Vm'lerden fayda çeşitli özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="117fc-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="117fc-138">Batch havuzları özel VM'ler ve düşük öncelikli sanal makineleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="117fc-139">bir havuzu oluşturulduğunda veya hello açık yeniden boyutlandırma işlemi veya Otomatik ölçek kullanarak mevcut bir havuz için herhangi bir zamanda değiştirildi VM her tür hello sayısı belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="117fc-140">İş ve görev gönderimi değişmeden kalır ve hello havuzunda hello VM türleriyle endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="117fc-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="117fc-141">Ayrıca, bir havuz tamamen kullanın düşük öncelikli sanal makineleri toorun işleri mümkün, ancak özel VM'ler yukarı döndürme olarak ailenin hello kapasite çalışan işleri korumak için en düşük eşiğin altına düşerse olası toohave unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="117fc-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="117fc-142">Batch havuzlarının otomatik olarak toohello hedef düşük öncelikli VM'lerin sayısını arama.</span><span class="sxs-lookup"><span data-stu-id="117fc-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="117fc-143">VM'ler etkisiz, toplu işlem kapasitesi ve dönüş toohello hedef kayıp tooreplace hello deneyecek.</span><span class="sxs-lookup"><span data-stu-id="117fc-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="117fc-144">Kesintiye görevleri Hello durumda toplu algılar ve otomatik olarak disablecomputenodeschedulingoption görevleri toobe yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="117fc-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="117fc-145">Düşük öncelikli sanal makineleri özel VM'ler farklı bir çekirdek kotası var.</span><span class="sxs-lookup"><span data-stu-id="117fc-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="117fc-146">düşük öncelikli sanal makineleri daha az maliyet olduğundan hello teklif düşük öncelikli VM'ler için özel VM'ler, yüksektir.</span><span class="sxs-lookup"><span data-stu-id="117fc-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="117fc-147">Bkz: [Batch Hizmeti kotaları ve sınırlarına](batch-quota-limit.md#resource-quotas) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="117fc-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="117fc-148">Düşük öncelikli sanal makineleri şu anda desteklenmemektedir hello havuzu ayırma modu ayarlandığı çok Batch hesapları için[kullanıcı aboneliği](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="117fc-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="117fc-149">Oluşturma ve havuzları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="117fc-149">Create and update pools</span></span>

<span data-ttu-id="117fc-150">Batch havuzundaki (Ayrıca başvurulan tooas işlem düğümleri) hem adanmış hem de düşük öncelikli sanal makineleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="117fc-151">Hem özel hem de düşük öncelikli VM'ler için hello hedef işlem düğümü sayısını ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="117fc-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="117fc-152">Merhaba düğümlerin hedef sayısını belirtir hello numarası toohave hello havuzunda istediğiniz Vm'leri.</span><span class="sxs-lookup"><span data-stu-id="117fc-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="117fc-153">Örneğin, bir Azure bulut hizmeti VM'ler 5 hedefle kullanarak havuzu toocreate VM'ler ve 20 düşük öncelikli sanal makineleri ayrılmış:</span><span class="sxs-lookup"><span data-stu-id="117fc-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="117fc-154">VM'ler ve 20 düşük öncelikli sanal makineleri toocreate 5 bir hedef Azure sanal makinelerini (Bu durumda Linux VM'ler) kullanarak havuzu bir adanmış:</span><span class="sxs-lookup"><span data-stu-id="117fc-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="117fc-155">Hem özel hem de düşük öncelikli VM'ler için hello geçerli düğüm sayısını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="117fc-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="117fc-156">Merhaba düğümü adanmış veya düşük öncelikli bir VM ise havuz düğümleri özelliği tooindicate vardır:</span><span class="sxs-lookup"><span data-stu-id="117fc-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="117fc-157">Bir veya daha fazla düğüm havuzunda etkisiz, havuzu üzerinde bir liste düğümleri işlemi hala düğümleri döndürür, düşük öncelikli düğüm geçerli sayısını hello değişmeden kalır, ancak bu düğüm varsa durumlarına toothe ayarlamak **geçersiz kılındı**durumu.</span><span class="sxs-lookup"><span data-stu-id="117fc-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="117fc-158">Toplu toofind değiştirme VM'ler deneyecek ve hello düğümleri Git başarılı olursa, **oluşturma** ve ardından **başlangıç** durumları görev yürütme için kullanılabilir hale gelmeden önce olduğu gibi yeni düğümler.</span><span class="sxs-lookup"><span data-stu-id="117fc-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="117fc-159">Düşük öncelikli sanal makineleri içeren bir havuzu ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="117fc-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="117fc-160">Yalnızca özel VM'ler oluşan havuzlarıyla gibi hello boyutlandırma yöntemini çağırarak veya Otomatik ölçek kullanarak olası tooscale bir havuz içeren düşük öncelik VM'ler değil.</span><span class="sxs-lookup"><span data-stu-id="117fc-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="117fc-161">Merhaba havuzu yeniden boyutlandırma işlemi değerini güncelleştiren bir ikinci isteğe bağlı parametresi alan **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="117fc-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="117fc-162">Merhaba havuzu otomatik ölçeklendirme formülü aşağıdaki gibi düşük öncelikli sanal makineleri destekler:</span><span class="sxs-lookup"><span data-stu-id="117fc-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="117fc-163">Almak veya ayarlamak hello değişkenin değeri olarak hello hizmet tanımlı **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="117fc-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="117fc-164">Merhaba hello hizmet tanımlı değişkenin değerini alabilir **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="117fc-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="117fc-165">Merhaba hello hizmet tanımlı değişkenin değerini alabilir **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="117fc-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="117fc-166">Bu değişken döndürür. hello hello düğümlerin sayısı durumu etkisiz ve yukarı veya aşağı hello kullanılamaz etkisiz düğüm hello sayısını bağlı olarak ayrılmış düğüm sayısını ölçeklendirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="117fc-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="117fc-167">İşler ve görevler</span><span class="sxs-lookup"><span data-stu-id="117fc-167">Jobs and tasks</span></span>

<span data-ttu-id="117fc-168">İşlerini ve görevleri düşük önceliğe düğümleri için çok az desteği gerektirir; Merhaba yalnızca desteği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="117fc-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="117fc-169">Merhaba JobManagerTask özelliği bir işin sahip yeni bir özellik **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="117fc-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="117fc-170">Bu özelliği true olduğunda hello iş yöneticisi görevi ya da bir adanmış veya düşük öncelikli düğümünde zamanlanabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="117fc-171">Bu özellik false ise, hello iş yöneticisi görevi yalnızca ayrılmış düğüm zamanlanmış tooa olacaktır.</span><span class="sxs-lookup"><span data-stu-id="117fc-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="117fc-172">Bir [ortam değişkeni](batch-compute-node-environment-variables.md) düşük öncelikli veya ayrılmış bir düğümde çalışan olup olmadığını belirleyebilmek kullanılabilir tooa görev uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="117fc-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="117fc-173">AZ_BATCH_NODE_IS_DEDICATED Hello ortam değişkenidir.</span><span class="sxs-lookup"><span data-stu-id="117fc-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="117fc-174">Önalım işleme</span><span class="sxs-lookup"><span data-stu-id="117fc-174">Handling preemption</span></span>

<span data-ttu-id="117fc-175">Sanal makineleri bazen etkisiz; Bu gerçekleştiğinde, toplu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="117fc-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="117fc-176">Merhaba etkisiz VM'ye sahip çok güncelleştirilmiş durumlarına**geçersiz kılındı**.</span><span class="sxs-lookup"><span data-stu-id="117fc-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="117fc-177">Görevler çalışıyormuş bu görevleri yeniden kuyruğa ve yeniden çalıştırın. ardından hello düğümü VM'ler etkisiz.</span><span class="sxs-lookup"><span data-stu-id="117fc-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="117fc-178">Merhaba VM etkili bir şekilde hello kaybolmasına VM üzerinde yerel olarak depolanan tooany veriler baştaki silinir.</span><span class="sxs-lookup"><span data-stu-id="117fc-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="117fc-179">Merhaba havuzu tooreach hello düşük öncelikli düğüm sayısını kullanılabilir sürekli olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="117fc-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="117fc-180">Yedek kapasite bulunduğunda, düğümlerin kimlikleri tutmak ancak, oluşturulmak yeniden başlatılır **oluşturma** ve **başlangıç** görev zamanlama için kullanılabilir önce belirtir.</span><span class="sxs-lookup"><span data-stu-id="117fc-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="117fc-181">Önalım sayıları hello Azure portal'ın bir ölçü olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="117fc-182">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="117fc-182">Metrics</span></span>

<span data-ttu-id="117fc-183">Yeni ölçümleri hello kullanılabilir [Azure portal](https://portal.azure.com) düşük öncelikli düğümleri için.</span><span class="sxs-lookup"><span data-stu-id="117fc-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="117fc-184">Bu ölçümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="117fc-184">These metrics are:</span></span>

- <span data-ttu-id="117fc-185">Düşük öncelikli düğüm sayısı</span><span class="sxs-lookup"><span data-stu-id="117fc-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="117fc-186">Düşük öncelikli çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="117fc-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="117fc-187">Etkisiz düğüm sayısı</span><span class="sxs-lookup"><span data-stu-id="117fc-187">Preempted Node Count</span></span>

<span data-ttu-id="117fc-188">hello Azure portal tooview ölçümlerini:</span><span class="sxs-lookup"><span data-stu-id="117fc-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="117fc-189">Tooyour hello portalda Batch hesabı gidin ve Batch hesabınızın hello ayarlarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="117fc-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="117fc-190">Seçin **ölçümleri** hello gelen **izleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="117fc-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="117fc-191">Hello istediğiniz hello ölçümleri seçin **kullanılabilir ölçümler** listesi.</span><span class="sxs-lookup"><span data-stu-id="117fc-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Düşük öncelikli düğümleri için ölçümleri](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="117fc-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="117fc-193">Next steps</span></span>

* <span data-ttu-id="117fc-194">Okuma hello [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md), önemli bilgiler herkesin toouse toplu hazırlanıyor.</span><span class="sxs-lookup"><span data-stu-id="117fc-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="117fc-195">Merhaba makale Batch uygulamanızı oluştururken kullanabileceğiniz birçok API özellikleri Batch hizmeti kaynak havuzları, düğümleri, işler ve görevler ve hello gibi hakkında daha ayrıntılı bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="117fc-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="117fc-196">Merhaba hakkında bilgi edinin [Batch API'lerini ve araçları](batch-apis-tools.md) Batch çözümleri oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="117fc-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
